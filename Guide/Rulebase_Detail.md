Korean | [English](./Rulebase_Detail_Eng.md)  | [Home](../README_Eng.md)

## 룰기반주행 

## 알고리즘 개발 시작하기



### ■ 사전 조건

윈도우 7, 윈도우 10 에서만 시뮬레이터가 동작합니다. (64bit)


<br>

### ■ 개발 언어 및 에디터

개발 언어는 python 입니다. 그리고 특별한 에디터가 필요하지 않습니다. python 코드를 수정할 수 있는 단순 텍스트 에디터라면 무엇이든 가능합니다.

기존에 파이썬 언어를 사용해신 경험이 없으셔도 두려워 하지 마세요 !!

어차피 간단한 if 구문과 변수 값 할당, 사칙연산 정도면 충분합니다.


<br>

### ■ 로컬 개발 환경의 세팅

[Quick start](../QuickStart/Readme.md)  페이지를 참고하시기 바랍니다.


<br>

### ■ 프로그램 실행 방법

1. Algo.exe 실행합니다.

2. 소스 실행 (다운받은 소스는 drive_control.py 과 driving_client.py 이렇게 2개의 파일입니다.)
```bash
python driving_client.py
```

소스코드를 보시면 steering 값이 0 인 상태로 천천히 직진하도록 되어있기 때문에, 실행후 차가 앞으로 전진할 것입니다.

주어지는 센싱 값에 따라 제어를 수행하면서 차가 도로를 이탈하지 않고 주행하도록 하면 됩니다.

<br>

### ■ 소스코드의 구조
<img src='./Images/rule_based_diagram.png'>

driving_client.py 의 DrivingClient 클래스는 drive_control.py 의 DrivingController 클래스를 상속받고 있습니다.

이 중에 실제로 수정이 이루어지는 파일은 driving_client.py 이며, 이 파일만 업로드하여 제출하게 됩니다.

DrivingClass 의 생성자에서 while 구문으로 제어루프를 돌리고 있으며, 그 주기는 0.1 초 입니다.

이 값은 로컬에서 테스트 시에 변경이 가능하지만, 서버에서는 driving_client.py 파일만 받아서 서버에 존재하는 drive_control.py 와 결합하여 실행됩니다.

따라서 driving_client.py 이외의 수정은 서버에 반영 되지 않습니다.


<br>

### 당부사항

코드가 작성 가능한 부분은 import 구문. 생성자 부분, control_driving 메서드 내부 이렇게 제한 되어있습니다.

지정된 란에만 코드를 추가하여 주시기를 부탁드립니다. 추가로 아래의 내용에 허용됩니다.

- ‘self.half_road_limit’ 변수를 사용할 수 있습니다.

- ‘driving_client.py’ 파일에 custom 함수 또는 custom 클래스를 추가할 수 있습니다.



import 구문 추가시 기본적인 파이썬 패키지는 서버에도 설치가 되어있겠지만, 특별한 패키지 설치가 필요한 경우 알고리즘 경진대회 공식 메일(algo.contest@samsung.com)을 통하여 통하여 요청주시기 바랍니다.

<br>

### ■ 차량의 수집 /제어 정보
```python
def control_driving(self, car_controls, sensing_info):
```

control_driving 메서드의 sensing_info 파라미터를 통해 받는 정보는 다음과 같습니다.

<br>

### sensing_info.to_middle

도로의 중앙차선으로부터의 차량까지의 직선 거리(m) 입니다.

이 값이 양의 값(+) 이면 차가 도로의 오른쪽에, 음수값(-) 이면 도로의 왼쪽에 위치함을 의미합니다.

Ex) to_middle : -10.73 | Type : float

<img src='./Images/Airsim_distance_from_center.png'>


<br>

### sensing_info.collided

충돌했는지 여부. 장애물과 충돌상태에서 계속해서 가속을 하면 계속해서 False이며, 정지(속도 = 0) 하거나 충돌상태에서 벗어나면 False 로 바뀝니다.

Ex) collided : True | Type : bool


<br>

### sensing_info.speed

현재 차량의 속도 (km/h) 를 나타냅니다.

Ex) speed : 10.51 | Type : float


<br>

### sensing_info.moving_forward

목표지점을 항하여 정주행(True) 하고 있는지 역주행(False) 하고 있는 나타냅니다.

Ex) moving_forward : True | Type : bool


<br>

### sensing_info.moving_angle

도로의 방향에 얼마나 정렬(align) 되어있는지를 말해주는 각 입니다. 가령, 이 값이 0 인 경우 도로와 평행하게 주행하고 있음을 나타내고,

-30도 이면 정주행 방향에서 왼쪽으로 30도 방향으로 나아가고 있다는 의미이며, +30도 이면 정주행 방향에서 오른쪽으로 30도 방향으로 가고 있다는 의미입니다.

여기서 +/- 는 각도를 의미하는 것이지, 도로 중앙차선의 오른쪽/왼쪽 기준이 아님을 주의하시기 바랍니다.

Ex) moving_angle : -72.5 | Type : float


<img src='./Images/Airsim_dgree.png'>


<br>

### sensing_info.track_forward_angles

현재 위치 기준으로 차량 전방의 10개 구간에 대한 각도를 배열로 알려줍니다. 한개의 구간은 10m 이며, 총 10 개의 정보를 미리 알려주므로 전방의 100 m 까지 정보를 나타내 주는 것이라고 볼 수 있습니다.

각도가 + 일 경우 현재 차량위치에서 정주행 기준으로 오른쪽 방향 으로 기울어지는 각도이며, - 일 경우 왼쪽으로 기울어지는 각도이다.

예를 들어 이 값이 다음과 같이 들어왔다면, 오른쪽으로 휘어지는 도로가 이어짐을 알 수 있으며, 휘어지는 정도는 각도의 차이를 통하여 판단할 수 있습니다.

Ex) track_forward_angles : [4, 8, 12, 16, 20, 27, 43, 52, 55, 58] | Type : list [int]

<img src='./Images/Airsim_dgree_forward10.png'>
<img src='./Images/Airsim_dgree_forward_out.png'>


<br>

### sensing_info.lap_progress

Goal 지점 대비 얼마나 진행이 되었는지 percentage 로 보여줍니다. 100 이 되면 완주 한 것입니다.

Ex) lap_progress : 5.43 | Type : float


<br>

### sensing_info.track_forward_obstacles

전방 100m 까지의 장애물 정보를 배열로 알려줍니다.
<img src='./Images/ob_01.png'>

장애물이 없는 경우 배열 사이즈가 0 이며(empty), 장애물이 있으면 가까이 있는 것부터 차례로 배열에 추가 됩니다.

배열에 실려있는 정보는 장애물과의 거리, 그리고 장애물의 to_middle 정보입니다.

(to_middle 값은 도로의 왼쪽에 있으면 - 값, 오른쪽에서 있으면 + 값으로 표시)

<img src='./Images/Airsim_obstacle.png'>

<br>

장애물의 사이즈는 모든 맵에서 고정 길이 2 m 이며, to_middle 값 기준으로 좌우 1 m 라고 보시면 됩니다.

<img src='./Images/Airsim_obstacle_2.png>

Ex) track_forward_obstacles : [{'dist': 10.72, 'to_middle': 2.93}] | Type : list [dict]


<br>

### sensing_info.opponent_cars_info

전방 100m, 후방 100m 안에 있는 상대편 차량의 정보를 알려줍니다.

배열의 순서는 내 차와 가까이 있는 순으로 정렬하여 들어옵니다.

<img src='./Images/opp_01.png>

상대편 차량에 대해 주어지는 정보는 아래와 같습니다.

1) 상대 차량의 이름

2) 도로 중앙선 기준으로 내 차와의 거리 차이(전방에 있을 때는 +값, 후방에 있을 때는 -값)

3) 상대방 차량이 현재 도로 중앙에서 얼마나 떨어져서 주행하고 있는지(to_middle 값)

4) 상대편 차량의 속도

<br>
<img src='./Images/opp_02.png>
          
내 차량과 상대편 차량의 거리는 각 차의 중앙점을 기준으로 표시됩니다.

가령 상대방과 내 차의 거리가 +10 m 이고, 내 차와의 to_middle(중앙차로에서의 거리) 값이 비슷하다면 
각 차량의 길이를 고려했을 때 바로 내 차의 앞을 주행하고 있는 것이겠죠.          
          
<img src='./Images/opp_03.png>   
상대 차량이 전방에 있는 경우, 거리는 양수값으로 들어옵니다. 
숫자값은 m 단위 입니다.
          
<img src='./Images/opp_04.png>   
상대 차량이 후방에 있는 경우, 거리는 음수값으로 들어옵니다.

<img src='./Images/opp_05.png>   
곡선인 도로인 경우에도, 위의 이미지와 같이 도로 중앙선을 기준으로 거리를 측정하였습니다.
Ex) opponent_cars_info : [{'car_name': 'Car2', 'dist': -0.1, 'to_middle': 2.0, 'speed': -0.0}] | Type : list [dict]
<br>


### About road width

도로의 폭은 맵 별로 조금씩 차이가 납니다. 도로 이탈여부를 판단하기 위하여 도로폭을 사용하실 때에는 다음 변수값을 사용하시기 바랍니다. 이 값은 도로 절반 폭에 차량 절반 폭을 더한 값이며, 만약 도로가 10m 폭의 도로이면, 절반폭인 5 m + 차량절반폭(1.25m) 가 더해진 6.25 의 값을 가지고 있습니다.(부모 클래스에 멤버변수로 값을 담고 있기 때문에 위치에 상관없이 사용하실 수 있습니다.)

```python
                # road half width + car half width
                self.half_road_limit
```            

<br>

### ■ 차량제어

### car_controls.steering

steering 값이 + 값이면 오른쪽 방향으로 제어, steering 이 - 값이면 왼쪽 방향으로 제어가 이루어집니다.

값의 범위 : -1 에서 +1 의 값


<img src='./Images/Airsim_steering_wheel.png'>


<br>

### car_controls.throttle (Accelerator)

0 보다 큰 값은 전진을 의미하고, 0 보다 작은 값은 후진을 의미합니다. + 값에서의 기어는 속도에 따른 자동으로 변속이 이루어 집니다.

값의 범위 : -1 에서 +1 의 값


<br>

### car_controls.brake

브레이크는 0 에서 1 사이의 값을 받습니다. throttle 과 별개로 차를 정지하거나 감속할때 사용가능합니다.


<br>

## ■ 멀티플레이 가이드

### Step1. json 파일 생성

최초 시뮬레이터 실행시 하기와 같은 Choose Vehicle 이라는 메시지가 보이고

이때 "예(Y)"를 클릭하면 자동차 모드로 실행이 됩니다.

<img src='./Images/choose_vehicle.png'>



<br>
추가적으로 하기 경로에 settings.json 이라는 파일이 생성이 됩니다.

경로 : C:\Users\SDS\Documents\AirSim

파일 : settings.json


<br>

### Step2. json 파일 수정하기

■ 멀티플레이

- settings.json 파일을 열어서 기존 내용을 모두 지우고 하기 소스를 넣어줍니다.

```json
    {
     "SettingsVersion": 1.2,
     "SimMode": "Car",
     "Vehicles": {
        "Car1": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": -2, "Z": 0
         },
        "Car2": {
           "VehicleType": "PhysXCar",
           "X": 0, "Y": 2, "Z": 0
         }
      }
    }
```            

<br>

■ 싱글플레이

- 차량 한대로 다시 변경하는 방법은 하기와 같이 작성합니다.

```json
    {
     "SettingsVersion": 1.2,
     "SimMode": "Car"
    }
```            

<br>

### Step3. Python 파일 수정하기

### ■ 멀티플레이

- client python 파일이 2개 필요합니다. (driving_client.py 복사)
- 각각의 client python 파일 하단에 있는 player_name을 수정합니다.

```python
        def setting_player_name(self):
            player_name = ""   #조작할 차량의 이름을 기입
        return player_name
```
            
＊차량의 이름은 settings.json Vehicles 내 Car1, Car2 입니다. (변경 가능합니다.)


<br>

### ■ 싱글플레이

- 변경 없이 공백으로 두고 실행하면 됩니다.

<br>

### Step4. 차량 동시 운행

### ■ 멀티플레이

1) 시뮬레이터 실행 (Algo.exe)

2) 1번 Client python 실행 (player_name = "Car1")

3) 2번 Client python 실행 (player_name = "Car2")


<br>

### ■ 싱글플레이

1) 시뮬레이터 실행 (Algo.exe)

2) 1번 Client python 실행


<img src='./Images/two_car.png'>

<br>

### ■ 추가 기능

카메라 위치 변경

- 단축키 : 숫자 4

- 단축키 클릭시 하기와 같이 화면이 스위칭 됩니다.

Car1 View

<img src='./Images/car1_view.png'>

<br>
Car2 View

<img src='./Images/car2_view.png'>

※ 변경된 카메라 View에 따라서 좌측 상단의 state 값이 해당 차량의 상태값으로 변경되어 보여집니다.




<br>

### ■ 맵 소개

### First Map : Basic Round

- 난이도 (Difficulty) : ★★☆☆☆

- 도로폭 (Road width) : 10m

- 도로 길이 (Road length) : 1,360m

직선 코스와 완만한 커브로 이루어진 맵으로 트랙 위의 장애물을 피해 2바퀴를 돌면 완주!

튜토리얼 단계의 기본적인 주행 봇을 만들어 보기 위한 트랙입니다.

<img src='./Images/map1_1.png'>
<br>
<img src='./Images/map1_3.png'>
<br>
<br>


### Second Map : Speed Racing (1)

- 난이도 (Difficulty) : ★★☆☆☆

장애물이 없는 서킷 맵으로 긴 직선주로가 있어 속도 제어가 필수적입니다.

빠른 속도로 주행이 필요한 맵인만큼 차량 전복에 주의가 필요합니다.


### Second Map : Speed Racing (2)

- 난이도 (Difficulty) : ★★★☆☆

Speed Racing (1)에 장애물이 추가된 버전입니다.


- 도로폭 (Road width) : 16m

- 도로 길이 (Road length) : 1,860m

<img src='./Images/self_map4_2.png'>

<br>

### Third Map : Smurf Valley Map 

- 난이도 (Difficulty) : ★★★☆☆

- 도로 폭 (Road width) : 15m

- 도로 길이 (Road length) : 1,953m

6개의 급커브 구간이 있는 직선주로와 커브구간이 조화롭게 구성되어 있는 트랙

중간중간 큐브 형태의 장애물이 배치되어 있으며, 도로 폭이 넓지 않기 때문에

무리한 주행 설정은 차량 전복으로 인한 실격을 조심해야 합니다.

나무와 절벽으로 둘러쌓여있는 구간이 많기 때문에 잘못하면 완주하지 못할 수도 있습니다.

<br>
<img src='./Images/map2_1.png'>
<br>

<img src='./Images/map2_2.png'>


