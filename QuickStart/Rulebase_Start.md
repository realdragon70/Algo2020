## 룰기반주행 
-------------------
### 01. 사전 진행 내용

[Quick Start](./Readme.md) 에 있는 내용을 먼저 수행하시기 바랍니다.



### 02. 주행 소스코드 실행하기

주행 소스 를 받아서 실행해 보겠습니다.

시뮬레이터를 실행 후 파이썬 소스를 다음과 같이 실행합니다.
```
\rule\>python driving_client.py
```

시뮬레이터의 자동차가 움직이는것을 확인하실 수 있습니다.


driving_client.py 의 control_driving( ) 함수 부분이 알고리즘(룰)을 a작성하시는 부분입니다.

함수에서 받는 파라미터의 sensing_info 에 차량에서 수집하는 각종 정보가 담겨있고, car_controls 의 값을 변경하여 리턴함으로써 차를 제어 합니다. 이를 활용하여 코드를 작성하시면 됩니다.

만약 함수 외부에 상태를 저장할 필요가 생기는 경우 멤버변수 Area 에 변수를 추가하여 사용하시기 바랍니다.


```python
from drive_controller import DrivingController

class MyDrivingClient(DrivingController):
    def __init__(self):
        # =========================================================== #
        #  Area for member variables =============================== #
        # =========================================================== #
        # Editing area starts from here
        #

        self.is_debug = False
        self.collision_flag = True

        #
        # Editing area ends
        # ==========================================================#

        super().__init__()

    def control_driving(self, car_controls, sensing_info):

        # =========================================================== #
        #  Area for writing code about driving rule ================= #
        # =========================================================== #
        # Editing area starts from here
        #

        if self.is_debug:
            print("=========================================================")
            print("distance from center : {}".format(sensing_info.distance_from_center))
            print("right of the center: {}".format(sensing_info.right_of_center))

            print("collided: {}".format(sensing_info.collided))
            print("car speed: {} m/s".format(sensing_info.speed))

            print("is moving forward: {}".format(sensing_info.moving_forward))
            print("moving angle: {}".format(sensing_info.moving_angle))
            print("lap_progress: {}".format(sensing_info.lap_progress))
            print("track_forward_angles: {}".format(sensing_info.track_forward_angles))
            print("opponent_cars_info: {}".format(sensing_info.opponent_cars_info))
            print("=========================================================")


        #
        # Editing area ends
        # ==========================================================#
        return car_controls

if __name__ == '__main__':
    MyDrivingClient()

```


### NoControlError가 발생하는 경우

self.is_debug = True 이거나 많은 내용을 출력하는 경우, 특별한 조작 없이도 아래와 같은 오류가 발생할 수 있습니다.

```python
  Traceback (most recent call last):
    File "driving_client.py", line 75, in <module>
      client.run()
    File "D:\repo\pony-bot\rule\drive_controller.py", line 126, in run
      raise NoControlError('No control was performed within 100ms.')
  drive_controller.NoControlError: No control was performed within 100ms.
```     


이러한 경우에는, drive_controller.py 파일의 no_control_interval_limit 값을 큰 값으로 변경해주시기 바랍니다.
```python
    # drive_controller.py
    no_control_interval_limit = 2000
```


### 03. 키보드 모드 사용하기

시뮬레이터 실행 후 "F8" 키 입력 (방향키로 자동차 조작 가능합니다)

※ Client Python 실행 이후에는 "F8" 키 입력이 불가능하며 백스페이스키로 시뮬레이터 리셋 후 다시 가능합니다.


더 자세한 내용은 [상세가이드](./Rulebase_Detail.md)를 참고해 주세요.

<br><br>
--------------
<br><br>

## Rule-based Driving 
-------------------
### 01. Prerequisites

Please, follow the steps in the Get Simulator. [Quick Start](./Readme.md) 



### 02. Running the source code

Please download the source code and run from cmd prompt, after executing the simulator first.
```
\rule\>python driving_client.py
```

You will see your vehicle is moving in the simulator.

If you see this code block, control_dring() method is the place holder for the rule based algorithms.

The parameter of the method contains all the information from vehicles, by assigning and return values on car_controls, you can make your vehicle move as you want.

If you need to preserve certain state out side of while loop, you can add variables on member variables area.



```python
from drive_controller import DrivingController

class MyDrivingClient(DrivingController):
    def __init__(self):
        # =========================================================== #
        #  Area for member variables =============================== #
        # =========================================================== #
        # Editing area starts from here
        #

        self.is_debug = False
        self.collision_flag = True

        #
        # Editing area ends
        # ==========================================================#

        super().__init__()

    def control_driving(self, car_controls, sensing_info):

        # =========================================================== #
        #  Area for writing code about driving rule ================= #
        # =========================================================== #
        # Editing area starts from here
        #

        if self.is_debug:
            print("=========================================================")
            print("distance from center : {}".format(sensing_info.distance_from_center))
            print("right of the center: {}".format(sensing_info.right_of_center))

            print("collided: {}".format(sensing_info.collided))
            print("car speed: {} m/s".format(sensing_info.speed))

            print("is moving forward: {}".format(sensing_info.moving_forward))
            print("moving angle: {}".format(sensing_info.moving_angle))
            print("lap_progress: {}".format(sensing_info.lap_progress))
            print("track_forward_angles: {}".format(sensing_info.track_forward_angles))
            print("opponent_cars_info: {}".format(sensing_info.opponent_cars_info))
            print("=========================================================")


        #
        # Editing area ends
        # ==========================================================#
        return car_controls

if __name__ == '__main__':
    MyDrivingClient()

```


### NoControlError

If the self.is_debug = True or if you print a lot of content, the following error may occur without special operations.

```python
  Traceback (most recent call last):
    File "driving_client.py", line 75, in <module>
      client.run()
    File "D:\repo\pony-bot\rule\drive_controller.py", line 126, in run
      raise NoControlError('No control was performed within 100ms.')
  drive_controller.NoControlError: No control was performed within 100ms.
```     


In this case, change the no_control_interval_limit in the drive_controller.py file to a larger value.

```python
    # drive_controller.py
    no_control_interval_limit = 2000
```


### 03. Getting Started in Keyboard Mode

Run the simulator and press F8 (You can operate the car with the arrow keys.)

※ F8 button is not working while Python is running. If you want to use F8 button again, please reset the simulator by pressing backspace key.

For more information, please refer to the [detailed guide](./Rulebase_Detail.md).
