## Rule-based Driving 
-------------------
### 01. Prerequisites

Please, follow the steps in the [Quick Start - Get Simulator](./Readme.md)



### 02. Running the source code

 run from cmd prompt, after executing the simulator first.

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

For more information, please refer to the [detailed guide](./Rulebase_Detail_Eng.md).
