Korean | [English](./Auto_Guide_Advanced_Eng.md)  | [Home](../README.md)

### ■ Marina Bay Circuit 변경된 버전 소개 (본선용)

기존 Circuit 의 난이도를 완화하기 위하여 트랙의 일부 구간을 잘라내었습니다.
트랙의 변경된 부분은 다음과 같습니다.

<img src='./Images/marina_bay_map_revised.png'>
<br>

### ■ 주어진 트랙의 일부분을 학습 시키기

Marina Bay Circuit 의 사이즈가 크다 보니, 뒷부분으로 갈수록 학습에 어려움이 있습니다. 이를 해결하기 위하여, 내부적으로 구현된 Api 중에 setResetLocation() 함수를 가이드 드립니다.
해당 api 는 다음과 같습니다.

```
    setResetLocation( x coordinate, y coordinate, yaw of vehicle)
```    
            
기본 코드의 경우 한번의 에피소드 실행 후에, Reset()을 호출하여 처음 시작점으로 이동하게 되어있습니다. 이때, Reset() 호출 직후에, 차량을 특정 위치로 이동시키는 코드를 추가합니다.

이를 위하여 dqn_model.py 소스를 다음과 같이 수정하시면 됩니다.

```
    def run(self, time_limit_hour):
        ...

        # while 루프시작.
        while not finish:
            ...

            if done:
                ...

                self.client.reset()
                time.sleep(0.2)

                # ======================================================
                # 이 부분 추가
                self.client.setResetLocation(335.96, - 74.21, -51.82)
                check_point_index = 38

                # ======================================================

                ...

                # ======================================================
                # 이 부분 주석 처리
                # check_point_index = 0
                # ======================================================

                scores_per_episode = []
                cur_lab = 1
                half_complete_flag = False
                current_episode += 1

            if round(self.car_current_pos_x, 4) != round(self.car_next_pos_x, 4):
                backed_car_state = car_current_state
            car_prev_state = car_current_state
            car_current_state = car_next_state

            if time_limit_sec != 0 and time.time() - self.start_time > time_limit_sec:
                finish = True
            ##END OF LOOP
```
            
- self.client.reset() 이후에 self.client.setResetLocation() 호출
- check_point_index 변수에 원하는 값 할당하고, 이하에 있는 check_point_index = 0 주석처리

사용 편의를 위해, 몇몇 포인트의 해당 값을 미리 측정하여 두었습니다.

<img src='./Images/marina_bay_map_teleport_position.png'>


(1) 번 위치
```
self.client.setResetLocation(335.96, - 74.21, -51.82)
check_point_index = 38
```
            

(2) 번 위치
```
self.client.setResetLocation(184.70, - 163.81, 167.95)
check_point_index = 71
```            

(3) 번 위치
```
self.client.setResetLocation(39.66, - 625.08, - 79.56)
check_point_index = 140
```         

(4) 번 위치
```
self.client.setResetLocation(16.55, - 1073.64, 135.76)
check_point_index = 400
```            

(5) 번 위치
```
self.client.setResetLocation(-217.22,  - 470.09,102.12)
check_point_index = 482
```            

위의 그림에서 표시된 위치 이외의 위치를 구하고자 하시면, 
dqn_reward_tester.py 의 while 루프 안에서 다음 구문을 추가하여 로그로 값이 출력되게 하고, 키보드로 차를 주행하여 원하는 위치 차량의 옮겨 놓으신 후, 로그로 출력되는 x,y 좌표 및 check point 를 구하시면 됩니다.

```
print("current position:", car_current_state.kinematics_estimated.position.x_val, car_current_state.kinematics_estimated.position.y_val, check_point_index)
            
```
위 코드로 구해지는 정보는 , x 좌표, y 좌표, check_point_index 입니다.

그리고, 차량의 yaw 값은 현재 차량의 앞쪽 방향 각도인데, 이 값은 지도에 도로가 표시된 방향을 보시고 조정해주셔야 합니다. 시작 지점의 차 방향(지도상의 위쪽 방향)의 yaw 값이 0 으로 기준이 되고, 지도상의 도로 모양을 보시고, 좌측은 - 각도, 우측은 + 각도로 방향을 대략적으로 가늠 하신 후에 실제로 차를 이동시켜보시고 세부 조정을 하셔야 합니다. 
