Korean | [English](./Autonomous_Detail_Eng.md)

## 자율주행 

### ■ 자율주행 개요

자율주행은 머신러닝의 여러 기법중 강화학습을 사용합니다.

강화학습은 에이전트가 환경과 상호작용 하면서 스스로 학습하는 방식입니다. 에이전트는 어느 한 환경 상태에서 정책이라는 전략에 따라 행동을 하면서, 새로운 상태에 도달합니다. 그리고 그 행동에 대한 보상을 받습니다. 여기서 행동은 사용자가 조이스틱을 상하좌우로 움직이는 것과 같은 입력을 말합니다. 에이전트는 어떤 행동이 좋은 행동인지 알지 못하기 때문에, 우리가 작성한 보상함수를 통하여 행동의 적합성을 알도록 해줍니다.

본 대회에서는 학습을 위한 모델을 개발자가 직접 처음부터 설계하지는 않고, 이미 생성된 모델을 템플릿화 하여, 그 중에 하이퍼 파라미터 값과 보상함수 그리고 행동공간(Action space) 부분을 작성하도록 되어있습니다. 머신러닝에 대한 사전 지식이 없더라도, 모델이 선택 할 수 있는 행동들의 정의하고, 특정 행동을 장려하기 위한 적절한 보상을 제공하면서 모델을 학습시킬 수 있습니다. 내 자동차가 좀더 잘 주행 할 수 있도록 발전시키는 과정을 통하여 강화학습이 동작하는 원리를 이해할 수 있습니다.

<br>

### ■ 소스 코드의 구성

제공하는 소스코드의 기본적인 클래스 구성은 다음과 같습니다. DQNClient 클래스가 가 DQNAgent 클래스를 사용하는 구조이며, DQNClient 클래스가 제공하는 템플릿의 일부분을 하위클래스인 DQNCustomClient 에서 오버라이드하여 실행하는 구조입니다.

<img src='./Images/reinforcement_learning.png'>
<br>


사용자가 작성하는 파일은 dqn_custom_client.py 파일입니다. 
이 파일에서 training_duration 변수는 학습을 진행할 시간 설정이며, 0(무제한) 부터 시간단위로 설정할 수 있습니다. 
model/weight load option 부분에는 기존에 학습을 진행하여 저장했던 모델의 weight 값들을 로드하여 이어서 학습을 진행하고자 할 때 사용합니다. 튜닝파라미터, 행동공간 함수, 보상함수는 다음 단락에서 설명합니다.



해당 소스코드는 다음과 같습니다.

```Python
from dqn_model import DQNClient
from dqn_model import DQNParam
import math
import sys

# =========================================================== #
# Training finish conditions (hour)
# assign training duration by hour : 0(limit less), 1 (an hour), 1.5 (an hour and half) ...
# =========================================================== #
training_duration = 0

# =========================================================== #
# model/weight load option
# =========================================================== #
model_load = False
model_weight_path = "./save_model/.../dqn_weight_00.h5"


# ===========================================================

class DQNCustomClient(DQNClient):
    def __init__(self):
        dqn_param = self.make_dqn_param()
        super().__init__(dqn_param)

    # =========================================================== #
    # Tuning area (Hyper-parameters for model training)
    # =========================================================== #
    def make_dqn_param(self):
        dqn_param = DQNParam()
        dqn_param.discount_factor = 0.99
        dqn_param.learning_rate = 0.00025
        dqn_param.epsilon = 1.0
        dqn_param.epsilon_decay = 0.999
        dqn_param.epsilon_min = 0.01
        dqn_param.batch_size = 100
        dqn_param.train_start = 1000
        dqn_param.memory_size = 20000
        return dqn_param

    # =========================================================== #
    # Action Space (Control Panel)
    # =========================================================== #
    def action_space(self):
        # =========================================================== #
        # Area for writing code
        # =========================================================== #
        # Editing area starts from here
        #
        actions = [
            dict(throttle=0.6, steering=0.1),
            dict(throttle=0.6, steering=-0.1),
            dict(throttle=0.6, steering=0.2),
            dict(throttle=0.6, steering=-0.2),
            dict(throttle=0.6, steering=0)
        ]
        #
        # Editing area ends
        # ==========================================================#
        return actions

    def compute_reward(self, sensing_info):

        # =========================================================== #
        # Area for writing code
        # =========================================================== #
        # Editing area starts from here
        #
        thresh_dist = self.half_road_limit  # 4 wheels off the track
        dist = abs(sensing_info.to_middle)

        if dist > thresh_dist:
            reward = -1
        elif sensing_info.collided:
            reward = -1
        else:
            if dist > 5:
                reward = 0.1
            elif dist > 4:
                reward = 0.2
            elif dist > 3:
                reward = 0.4
            elif dist > 2:
                reward = 0.6
            elif dist > 1:
                reward = 0.8
            else:
                reward = 1

        #
        # Editing area ends
        # ==========================================================#
        return reward


if __name__ == "__main__":
    client = DQNCustomClient()

    if model_load:
        client.agent.load_model(model_weight_path)

    client.run(training_duration)
    sys.exit()
```

<br>        


### ■ DQN의 하이퍼 파라미터



discount_factor : 0에서 1 사이의 값으로 설정되며, 즉각적으로 주어지는 보상과 미래의 보상이 차이가 나도록 하기 위하여 사용합니다.



learning_rate: 학습된 가중치를 얼마만큼 한꺼번에 모델에 반영할 것인지에 대한 값 입니다. 학습에 있어서의 보폭에 해당합니다. 보폭이 너무 크면 최적의 지점을 그냥 지나칠 수도 있고, 보폭이 너무 작으면 학습 시간이 오래걸립니다.



epsilon : Epsilon Greedy 정책에 따라 행동을 선택합니다. 즉, 초반에는 Epsilon 값이 1.0 이기 때문에, agent의 행동이 전적으로 random 선택이 되고, epsilon 값이 감소 함에 따라 model 을 통하여 행동을 결정하는 비율이 높아집니다.

epsilon_decay : Epsilon 값이 감쇠하는 비율입니다.

epsilon_min : Epsilon 값이 감쇠하더라도 최소 값을 유지하도록 합니다. Epsilon 이 완전히 0이 되는 것을 방지하여, 최소한의 랜덤한 탐색이 이루어지도록 합니다.



batch_size: 한번 훈련할때 replay memory 에서 추출하는 데이터의 갯수

train_start: 훈련을 시작하는 시점. Replay memory 에 어느정도 데이터가 쌓여 있어야 랜덤추출이 의미가 있으므로, 데이터가 쌓일때 까지 훈련 시작시점을 지연시킵니다.

memory_size: 환경과 상호작용하면서 얻는 데이터는 유사한 연속된 데이터가 많습니다. 이 데이터를 가지고 곧바로 학습을 하게되면 문제가 있는데, 가령 에이전트가 안 좋은 상황에 빠졌을 때 그 상황에 맞게 학습이 이루어 진다는 문제가 있습니다. 따라서, 입력 데이터간의 상호간섭을 줄이기 위하여 Replay memory 라는 공간에 경험를 쌓아놓고 무작위로 추출해서 학습합니다. 여기서 지정하는 값이바로 이 경험 리플레이 공간의 사이즈 입니다.

<br>

### ■ 보상(Reward) 함수

강화학습에서는 보상함수를 잘 설계하는 것이 학습에 매우 중요한 역할을 합니다. 보상은 차량이 트랙 위의 한 곳에서 다른 곳으로 이동할 경우 부여하는 피드백(보상 또는 페널티 점수)을 나타냅니다. 바람직한 이동일 때는 행동이나 상태에 대하여 높은 점수를 매기고, 잘못되거나 소모적인 이동일 때는 낮은 점수를 매김으로써, 차량이 우리가 원하는 방향으로 이동하도록 유도합니다.



보상함수의 signature 는 다음과 같습니다.

```Python
                def compute_reward(self, sensing_info):
                    #...
                    # 상황에 대한 적절한 reward 값 할당
                    if abs(sensing_info.to_middle) < 5:
                        reward = 1
                    else:
                        reward = -1
                return reward
```


<br>

### ■ 보상 함수에서 사용 가능한 상태 정보

보상 함수의 파라미터인 sensing_info는 시뮬레이터 차량에서 수집된 상태 정보들을 가지고 있습니다. 이 정보들을 가지고, 현재 상태에 대한 Reward 를 적절히 부여 할 수 있습니다.

<br>

### sensing_info.to_middle

도로의 중앙차선으로부터의 차량까지의 직선 거리(m) 입니다. 이 값이 양의 값(+) 이면 차가 도로의 오른쪽에, 음수값(-) 이면 도로의 왼쪽에 위치함을 의미합니다.

Ex) to_middle : -10.73 | Type : float

<img src='./Images/Airsim_distance_from_center.png'>

<br>


### sensing_info.collided

충돌했는지 여부. 장애물과 충돌상태에서 계속해서 가속을 하면 계속해서 False이며, 정지(속도 = 0) 하거나 충돌상태에서 벗어나면 False 로 바뀝니다.

Ex) collided : True | Type : bool

<Br>

### sensing_info.speed

현재 차량의 속도 (km/h) 를 나타냅니다.

<br>

### sensing_info.moving_forward

목표지점을 항하여 정주행(True) 하고 있는지 역주행(False) 하고 있는 나타냅니다.

Ex) moving_forward : True | Type : bool

<br>

### sensing_info.moving_angle

도로의 방향에 얼마나 정렬(align) 되어있는지를 말해주는 각 입니다. 가령, 이 값이 0 인 경우 도로와 평행하게 주행하고 있음을 나타내고, -30도 이면 정주행 방향에서 왼쪽으로 30도 방향으로 나아가고 있다는 의미이며, +30도 이면 정주행 방향에서 오른쪽으로 30도 방향으로 가고 있다는 의미입니다. 여기서 +/- 는 각도를 의미하는 것이지, 도로 중앙차선의 오른쪽/왼쪽 기준이 아님을 주의하시기 바랍니다.

Ex) moving_angle : -72.5 | Type : float

<img src='./Images/Airsim_dgree.png'>

<br>


### sensing_info.track_forward_angles

현재 위치 기준으로 차량 전방의 10개 구간에 대한 각도를 배열로 알려줍니다. 한개의 구간은 10m 이며, 총 10 개의 정보를 미리 알려주므로 전방의 100 m 까지 정보를 나타내 주는 것이라고 볼 수 있습니다. 역시 각도가 + 일 경우 현재 차량위치에서 정주행 기준으로 오른쪽 방향 으로 기울어지는 각도이며, - 일 경우 왼쪽으로 기울어지는 각도이다. 예를 들어 이 값이 다음과 같이 들어왔다면, 오른쪽으로 휘어지는 도로가 이어짐을 알 수 있으며, 휘어지는 정도는 각도의 차이를 통하여 판단할 수 있습니다.



Ex) track_forward_angles : [4, 8, 12, 16, 20, 27, 43, 52, 55, 58] | Type : list [int]

<img src='./Images/Airsim_dgree_forward10.png'>


<br>


### sensing_info.lap_progress

Goal 지점 대비 얼마나 진행이 되었는지 percentage 로 보여줍니다. 100 이 되면 완주 한 것입니다.

Ex) lap_progress : 5.43 | Type : float

<br>

### sensing_info.track_forward_obstacles

전방 100m 까지의 장애물 정보를 배열로 알려줍니다.

장애물이 없는 경우 배열 사이즈가 0 이며(empty), 장애물이 있으면 가까이 있는 것부터 차례로 배열에 추가 됩니다.

배열에 실려있는 정보는 장애물과의 거리, 그리고 장애물의 to_middle 정보입니다.

(to_middle 값은 도로의 왼쪽에 있으면 - 값, 오른쪽에서 있으면 + 값으로 표시)


<img src='./Images/Airsim_obstacle.png'>

<br>


장애물의 사이즈는 모든 맵에서 고정 길이 2 m 이며, to_middle 값 기준으로 좌우 1 m 라고 보시면 됩니다.

<img src='./Images/Airsim_obstacle_2.png'>

Ex) track_forward_obstacles : [{'dist': 10.72, 'to_middle': 2.93}] | Type : list [dict]

<br>

### About road width

도로의 폭은 맵 별로 조금씩 차이가 납니다. 도로 이탈여부를 판단하기 위하여 도로폭을 사용하실 때에는 다음 변수값을 사용하시기 바랍니다. 이 값은 도로 절반 폭에 차량 절반 폭을 더한 값이며, 만약 도로가 10m 폭의 도로이면, 절반폭인 5 m + 차량절반폭(1.25m) 가 더해진 6.25 의 값을 가지고 있습니다.(부모 클래스에 멤버변수로 값을 담고 있기 때문에 위치에 상관없이 사용하실 수 있습니다.)

```Python
                # road half width + car half width
                self.half_road_limit
            
```

<br>


### ■ 보상 함수 작성 예제

예제1) 충돌하거나 도로를 이탈했을때 낮은 점수(페널티) 부여하기

```Python
    def compute_reward(self, sensing_info):

        reward = 1
        thresh_dist = self.half_road_limit  # 4 wheels off the track

        dist = abs(sensing_info.to_middle)

        if dist > thresh_dist:
            reward = -1
     elif sensing_info.collided:
            reward = -1

     return reward
```
<br<



예제2) 트랙 중앙을 따라 주행하도록 유도하기


```python

    def compute_reward(self, sensing_info):

        dist = abs(sensing_info.to_middle)
          if dist > 5:
                reward = 0.1
            elif dist > 4:
                reward = 0.2
            elif dist > 3:
                reward = 0.4
            elif dist > 2:
                reward = 0.6
            elif dist > 1:
                reward = 0.8
            else:
                reward = 1

     return reward
```

<br>


### ■ 행동 공간 함수

어떤 상태를 입력으로 차량이 받아 취할 수 있는 행동(action) set 을 정의합니다. 이 행동 공간에서 차량의 조향(steering) , throttle 값의 조합을 정의하여 놓고 사용하게 됩니다. 기본값으로 5가지 액션을 정의하여 놓았지만, 사용자의 판단에 따라 액션의 갯수를 늘리거나 속성을 수정하여 훈련하여야 합니다. 가령 급격한 코너 구간이 있는 경우, 큰 조향값이 포함되어야 할 수 있고, 직선주로에서는 좀더 가속을 하고 싶다면 steering = 0 일때,throttle 에 더 큰 숫자를 넣을 수 있습니다. 행동의 갯수가 늘어남에 따라 학습시간이 늘어나거나 일정 수준 이상의 학습이 이루어지지 않을 수 있음을 유의하시기 바랍니다.



힌트) 조향 각은 -1 에서 1 까지의 값을 사용할 수 있지만, 현재 제공하는 맵에서 통상적으로 -0.5 ~ 0.5 까지의 범위의 값이면 충분합니다. 도로의 폭이 넓지 않기 때문에, 그 이상의 값을 사용할 경우에 쉽사리 도로를 이탈합니다. 그리고 빠른 속도를 지정한 모델은 코너링이 어렵기 때문에, 느린 속도를 지정한 모델보다 수렴하는데 더 오래 걸립니다. throttle 값은 0 ~ 1 값을 사용합니다. 이때 throttle 값은 고정으로 세팅하는 것이 학습에 유리합니다. 리워드 함수를 어느정도 안정화 시킨 이후에 점차 속도를 높여가며 학습을 시도해 보시기를 권장합니다


행동공간함수 예제)
```python

     def action_space(self):
        # =========================================================== #
        # Area for writing code
        # =========================================================== #
        # Editing area starts from here
        #
        actions = [
            dict(throttle=0.6, steering=0.1),
            dict(throttle=0.6, steering=-0.1),
            dict(throttle=0.6, steering=0.2),
            dict(throttle=0.6, steering=-0.2),
            dict(throttle=0.6, steering=0)
        ]
        #
        # Editing area ends
        # ==========================================================#
        return actions
```

<br>

### ■ 학습중 리워드 관찰하기

학습된 리워드의 총 합은 계속해서 업데이트가 이루어지며, save_graph/{시간폴더}/ 이하에 airsim_dqn_00.png 이름의 그래프로 기록이 됩니다.

학습된 리워드 총합이 증가하는 방향(우 상향) 으로 되어야 원하는 방향으로 수렴하고 있다고 볼 수 있으며, 그렇지 않을 경우 더 학습하여도 의미가 없을 가능성이 높습니다.

<br>

<img src='./Images/airsim_dqn_graph_1.png'>

<br>



### ■ 학습된 가중치를 저장하기

학습된 가중치 파일은 save_model/{시간폴더}/ 이하에 airsim_dqn_00.h5 파일이며, 홈페이지 상에 실제로 업로드 하게 되는 파일이 이 가중치 파일입니다. 가중치 파일은 10개 에피소드 마다 번호를 달리하여 저장이 이루어 지도록 되어있습니다. 주의 하실 점은 학습된 가중치는 동작 공간(Action space) 가 동일한 조건 하에서만 로드하여 사용할 수 있다는 것입니다. 모델을 학습 시킨 이후에 동작공간을 변경하면, 학습된 내용의 맥락이 바뀌기 때문에 저장한 가중치는 정상동작하지 않을 것이라는 점을 기억하시기 바랍니다.

<br>

### ■ 학습한 모델을 평가하기

시뮬레이터를 구동한 상태에서 dqn_evaluator.py 를 실행하면, 지정한 경로(save_model/{시간폴더}/ airsim_dqn_00.h5) 에 있는 가중치 파일을 로드하여 주행 해 볼 수 있습니다. 주행은 총 3회를 시도하게 되며, 3회중에 몇번을 완주에 성공했는지, 각각의 lap time 을 보여줍니다. 5번 모두 실패하는 경우, lap time 은 보여주지 않습니다. 이후 홈페이지에 제출하여 평가하는 경우에는, 3번의 시도 중에 가장 최고 기록을 취하게 됩니다.

<br>

### ■ 학습한 모델을 제출하기

생성한 모델에 대한 훈련이 충분히 이루어졌다고 생각하면, 홈페이지의 팀 메뉴에서 학습된 모델을 제출 할 수 있습니다. (자세한 제출 방법은 7/1 정식 오픈 이후 가이드해드릴 예정입니다.)

<br>

### ■ 맵 소개

학습을 위한 맵을 단계별로 제공합니다.


### Tutorial Map (1):

거의 직선 주로에 가까운 도로에서 중앙선을 따라 달리는 연습을 해보시기 바랍니다.

<img src='./Images/self_map1_1.png'> <img src='./Images/self_map1_2.png'>

### Tutorial Map (2):

2단계는 좀더 곡선이 많은 도로이며, Reward 함수를 통하여 점차 개선된 모델을 가지고, 2 단계에 도전 하실 수 있습니다.


<img src='./Images/self_map2_1.png'><img src='./Images/self_map2_2.png'>


## Basic Round - (1) :

- 난이도 (Difficulty) : ★☆☆☆☆

- 도로폭 (Road width) : 10 m

- 도로 길이 (Road length) : 1,360m

직선 코스와 완만한 커브로 이루어진 맵으로 장애물이나 시야를 막는 오브젝트가 없습니다.

Tutorial Map 에서 안정적으로 학습을 해보셨다면, 이 맵에서 본격적인 주행에 도전하여 보시기 바랍니다.

이 단계를 안정적으로 주행한다면, 해당 모델의 weight 를 제출하여, 본인의 기록을 타인의 기록과 비교하실 수 있습니다. (7월1 일 이후 제공)


<img src='./Images/self_map3_1.png'><img src='./Images/self_map3_2.png'>



## Basic Round - (2) :

- 난이도 (Difficulty) : ★★☆☆☆

- 도로폭 (Road width) : 10 m

- 도로 길이 (Road length) : 1,360m

Basic Round 1번 맵에서 장애물이 추가된 맵 입니다.

해당 맵에서 장애물에 대해 학습해 보시기 바랍니다.

<img src='./Images/self_map3_4.png'>

<br>


## Speed Racing :

- 난이도 (Difficulty) : ★★☆☆☆

- 도로폭 (Road width) : 16 m

- 도로 길이 (Road length) : 1,860m

장애물이 없는 서킷 맵으로 긴 직선주로가 있어 속도 제어가 필수적입니다.

빠른 속도로 주행이 필요한 맵인만큼 차량 전복에 주의가 필요합니다.

<img src='./Images/self_map4_2.png'>

