[Korean](./Rulebase_Detail.md) | English  | [Home](../README_Eng.md)

## Rule-based Driving 

## Beginning algorithm development



### ■ Pre-condition

The simulator works only on Windows 7 and Windows 10 64bit.

Only the “ Document ” folder path and Windows user account “ English ” are supported.

When using OneDrive, please refer to https://github.com/microsoft/AirSim/issues/1066.


<br>

### ■  Development language and editor

The development language is available in python, java, cpp.

For basic driving, a simple if construct, variable value allocation, and quadrature operation are sufficient.


<br>

### ■ Local development environment setting (Simulator)

For more information on installing the simulator, see Quick start posting on the bulletin board.

[Quick start page.](../QuickStart/Readme_Eng.md) 


<br>

### ■ (Java) Local development environment setting

When developing in Java language, we need tools to develop jdk (1.8 or more) installation and java code.

For jdk, need 1.8 or more version.

For current driving bot, we are providing project files for immediate development via Intellij. (It is also possible to modify and execute the source through presence. In the case of Eclipse, after configuring workspace, select the bot _ java\ v1 folder through File > Open project from File System and load the project. )


<br>

### ■ (Java) Running method

1. Run the simulator. (One person driving: run.bat, multiple driving: runsv.bat)

2. Run the driving bot.

It is necessary to run MyCar.java in the Bot_java v1 folder of the downloaded MyCar.

Here, let me explain how to run through the IntelliJ tool.

Select and open the downloaded MyCar's Bot_java v1 folder.

<img src='./Images/java_detail_guide_1.jpg'>

Run the source (MyCar.java). It will run after the build. If

<img src='./Images/java_detail_guide_2.jpg'>

If you look at the source code, the car will move forward after execution because it is supposed to slowly go straight with the target value 0.

You can make sure that the car does not leave the road while performing control according to the given sensing value.


<br>

### ■ Structure of (Java) source code

It has a built-in DrivingInterface module (DrivingInterface.dll) to control the drive. The DrivingInterface calls the control _ driving function in the MyCar class at 0.1 second intervals. (For reference, the DrivingInterface.java file is a class that processes and delivers data transmitted by the DrivingInterface module for easy reference by developers.) )

In fact, the file where the modification is made is MyCar.java, and only this file is uploaded and submitted.

Modifications other than MyCar.java are not reflected on the server.


<br>

### ■ (Java) (Refer)

The part where the code can be written is so limited within the member variable portion within MyCar.java, within the control _ driving method.

Please add code only to the specified place. In addition, it is allowed in the content below.

- You can use the ‘ trust_info.half_road_limit ’ variable.

- You can add a query function or class to the ‘ MyCar.java ’ file.

When adding an import syntax, the basic package is installed on the server, but if you need to install a special package, please contact the conference bulletin board.


<br>

### ■ (Python) Local development environment setting

Developing in Python language does not require a separate IDE. It can be used as a memo pad, but we provide project files so that it can be developed directly through pycharm.


<br>

### ■ (Python) driving execution method

1. Run the simulator. (One person driving: run.bat, multiple driving: runsv.bat)

2. Run the driving bot.

3. It is necessary to run my_car.py in the Bot _ python v1 folder of MyCars downloaded.

4. Through Python my_car.py, it can be executed in the command window, and it can be executed directly in the Python tool.

5. Here, I will explain how to execute through the Pytens tool.

6. Select and open the Bot _ python v1 folder of MyCars.

<img src='./Images/python_detail_guide_1.jpg'>

Run the source (my _ car.py).

<img src='./Images/python_detail_guide_2.jpg'>

You can also run “python my_car.py” in the Command window.

If you look at the source code, the car will move forward after execution because it is supposed to slowly go straight with the target value 0.

You can make sure that the car does not leave the road while performing control according to the given sensing value.


<br>

### ■ Structure of (Python) source code

my_car.py's DrivingClient class inherits the drive_control.py's DrivingController class.

Among these, the file that is actually modified is my _ car.py, and only this file is uploaded and submitted.

In the DrivingClass constructor, the control loop is turned with a while syntax. Its cycle is 0.1 seconds.

This value can be changed when testing locally, but the server receives only my _ car.py file and runs in combination with drive _ control.py existing on the server.

Therefore, modifications other than my_car.py are not reflected on the server.


<br>

### ■ (Python) (Refer)

The part where the code can be created is the import syntax; the constructor portion, within the control _ driving method, is thus limited.

Please add code only to the specified place. In addition, it is allowed in the content below.

- You can use the ‘self.half_road_limit’ variable.

- You can add a query function or class to the ‘my_car.py’ file.

When adding an import syntax, the basic python package is installed on the server, but if you need to install a special package, please ask through the conference bulletin board.


<br>

### ■ (C++) Setting local development environment

When developing in C++ language, we need tools to install windows sdk 8.1 and develop C + + code and create executable files.

For the current driving bot, the project file is being provided so that it can be developed immediately via Visual Basic 2017.

To install Windows sdk 8.1, you can proceed as follows.

After running Visual installer, select windows 8.1 sdk to proceed with installation.

If you do not have a license, we encourage you to use Visual Studio Express 2017. (vs_WDExpress.exe)

<img src='./Images/cpp_detail_guide_1.png'>

Windows 8.1.

After selecting SDK and UCRT SDK, proceed with the modification. (If it is already done, it can be omitted.) Otherwise, proceed with installation as a separate installation file. (sdksetup.exe)

<img src='./Images/cpp_detail_guide_2.jpg'>

If you are using the revised version, download the windows 8.1 SDK from MS site and proceed with installation.


<br>

### ■ (C++) Running method

1. Run the simulator. (One person driving: run.bat, multiple driving: runsv.bat)

2. Run the driving bot.

It is necessary to build and run MyCar.vcxSettings in the Bot_cpp v1 folder of the downloaded MyCars.

Here I will explain how to run through Visual Basic 2017 tool.

Double-click the MyCar.vcxfolder in the Bot_cpp v1 folder of the downloaded MyCar or open it in Visual Stuido 2017 through an open project menu.

Run the source (MyCar.cpp). It will run after the build.

You can also run using the created MyCar.exe (\MyCar\Bot _ Cpp\v1\DrivingInterface\Build\Release\MyCar.exe).

After setting the build configuration to Release (or debug) or x64, select the solution file and execute the solution build (or through the build menu in the menu). When the build is successfully completed, it runs through the Start (or Start Debugging) menu without debug in the Debug menu.

<img src='./Images/cpp_detail_guide_3.jpg'>

If you look at the source code, the car will move forward after execution because it is supposed to slowly go straight with the target value 0.

You can make sure that the car does not leave the road while performing control according to the given sensing value.


<br>

### ■ (C++) Structure of source code

It has a built-in DrivingInterface module (DrivingInterface.dll) to control the driving. The DrivingInterface calls the control _ driving function every 0.1 second.

In fact, the file that is modified is MyCar.cpp, and only this file is uploaded and submitted.

Modifications other than MyCar.cpp are not reflected on the server.


<br>

### ■ (C++) (refer)

The part where the code can be created can be configured as a variable within MyCar.cpp, and this is limited within the control _ driving method.

Please add code only to the specified place. In addition, it is allowed in the content below.

- You can use the ‘ trust_info.half_road_limit ’ variable.

- You can add a query function or class to the ‘ MyCar.cpp ’ file.


<br>

### ■ Vehicle collection / control information

The information received through the control_info parameter of the control_driving method is as follows.


<br>

### sensing_info.to_middle

The linear distance (m) from the middle lane of the road to the vehicle.

If this value is a positive value (+), then the car is located on the right side of the road, and if the negative value (-) is located on the left side of the road.

Ex) to_middle : -10.73 | Type : float

<img src='./Images/Airsim_distance_from_center.png'>


<br>

### sensing_info.collided

Whether or not there is a collision. If you continue to accelerate in the state of collision with an obstacle, it is False continuously, stop (speed)=0) or when out of conflict, it changes to False.

Ex) collided : True | Type : bool


<br>

### sensing_info.speed

Indicates the current speed of the vehicle (km / h).

Ex) speed : 10.51 | Type : float



<br>

### sensing_info.moving_forward

Indicates whether the target is destined for True or False.

Ex) moving_forward : True | Type : bool


<br>

### sensing_info.moving_angle

It is the angle that tells how much it is aligned in the direction of the road. For example, if this value is 0, it indicates that it is driving parallel to the road.

-30 degrees means that you are going 30 degrees to the left in the direction of the driving direction, and + 30 degrees means you are going 30 degrees to the right in the direction of the driving direction.

Please note that it is not the right / left standard of the road center lane.Ex) moving_angle : -72.5 | Type : float

Ex) moving_angle : -72.5 | Type : float


<img src='./Images/Airsim_dgree.png'>


<br>

### sensing_info.track_forward_angles


An array of angles for 10 sections in front of the vehicle based on its current location. One section is 10m, and it tells you a total of 10 pieces of information in advance, so it represents information up to 100m in front.

If the angle is +, it is an angle tilted in the right direction based on the driving direction at the current vehicle location, and if it is -, it is an angle tilted to the left.

For example, if this value comes in as follows, it can be seen that the road is bent to the right, and the degree of bending can be determined by the difference in angle.

Ex) track_forward_angles : [4, 8, 12, 16, 20, 27, 43, 52, 55, 58] | Type : list [int]

<img src='./Images/Airsim_dgree_forward10.png'>
<img src='./Images/Airsim_dgree_forward_out.png'>


<br>

### sensing_info.lap_progress

It shows how much progress has been made compared to Goal branch. When it is 100, it is finished.

Ex) lap_progress : 5.43 | Type : float


<br>

### sensing_info.track_forward_obstacles

It gives you an array of obstacle information up to 100 meters in front.

<img src='./Images/ob_01.png'>

If there is no obstacle, the array size is 0 (empty), and if there is an obstacle, it is added to the array from the nearest one.

The information in the array is the distance from the obstacle and the to _ middle information of the obstacle.

(The value to _ middle is displayed as - value if it is on the left side of the road, + value if it is on the right side)

<img src='./Images/Airsim_obstacle.png'>

<br>

The size of the obstacle is 2 m in fixed length on all maps, and 1 m in left and right based on the to _ middle value.

<img src='./Images/Airsim_obstacle_2.png'>


Ex) track_forward_obstacles : [{'dist': 10.72, 'to_middle': 2.93}] | Type : list


<br>

### sensing_info.opponent_cars_info

It gives you information about your opponent's vehicle 100 meters in front and 100 meters in back.

The order of the arrays is sorted in the order that they are close to my car.

<img src='./Images/opp_01.png'>


The information given to the other vehicle is as follows.

1. The name of the relative vehicle

2. Difference in distance from my car based on the road center line (+ value when in the front, + value when in the rear)

3. How far the other vehicle is currently driving from the center of the road (to _ middle value)

4. speed of the opposite vehicle

<br>
<img src='./Images/opp_02.png'>


The distance between my car and the other vehicle is indicated based on the center point of each car.

For example, if the distance between my car and the other car is + 10 m, and the value of the to middle with my car is similar, it is driving right in front of my car considering the length of each car.

<img src='./Images/opp_03.png'>

If the opponent vehicle is in the front, the distance is entered as a positive value. The numeric value is in m units.

<img src='./Images/opp_04.png'>

If the opponent vehicle is in the rear, the distance enters the negative value.
          
<img src='./Images/opp_05.png'>        

Even if it is a curved road, the distance is measured based on the center line of the road as shown in the image above.

Ex) opponent_cars_info : [{'car_name': 'Car2', 'dist': -0.1, 'to_middle': 2.0, 'speed': -0.0}] | Type : list


<br>

### sensing_info.distance_to_way_points
 
Provides 10 forward way-points and a straight distance to the vehicle.
 
Ex) distance_to_way_points : [2.98, 12.47, 22.42, 32.39, 42.34, 52.32, 62.26, 72.13, 81.83, 91.22] | Type : list [float64]

<img src='./Images/dist_to_waypoints_01.png'>   


<br>

### About road width

The width of the road is slightly different by map. When using road widths to determine whether or not to leave the road, use the following variable values. This value is a value that adds half width of the vehicle to half width of the road, and if the road is 10 m wide, it has a value of 6.25 that adds half width of 5 m + half width of the vehicle _ .25m). (Because the parent class contains a value as a member variable, you can use it regardless of location. )

```python
                # road half width + car half width
                (Java, cpp) sensing_info.half_road_limit
                (Python) self. half_road_limit
```            


<br>

### ■  Vehicle control

### car_controls.steering

Control in the right direction if the value is +, control in the left direction if the value is -.

Value range: -1 to +1


<img src='./Images/Airsim_steering_wheel.png'>


<br>

### car_controls.throttle (Accelerator)

A value greater than 0 means forward, and a value less than 0 means backward. The gears at the + value are automatically transformed according to the speed.

Value range: -1 to +1


<br>

### car_controls.brake

The brake receives a value between 0 and 1. Available when stopping or slowing down a car apart from throttle.


<br>

### penalty policy

If the road goes off to the inside wheels, the cleaning operation is applied inside the simulator. The Brake value is set to 0.9, which decelerates the vehicle speed.


<br>

## ■ Running Simulator Execution Guide

### Step1. creating json file

When executing the initial simulator, a message called Choose Vehicle is shown as follows

When you click "Yes", it will run in car mode.

<img src='./Images/choose_vehicle.png'>

In addition, a file called settings.json is created in the following path.
(User account: SDS case)

Path : C:\Users\SDS\Documents\AirSim

File : settings.json


<br>

### Step2. Modifying json file

■ Multiplay

- Open the settings.json file to clear all existing contents and put the following source.

- This is an example of 4 vs. (You can adjust the number of seats from 2 to 4 units, and adjust the vehicle location, X, Y, Z)

Json file sample and description

In the case of "Map", the type of obstacle configuration is shown.

The “ Map ” may have one of “ 1 ”, “ 2 ” or “ 3 ”.

If not defined, one of 1 to 3 obstacles is set arbitrarily.

```json
    {
     "SettingsVersion": 1.2,
     "SimMode": "Car",
     "Algo": {
        "Map": "1"
     },
     "Vehicles": {
        "Car1": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": -6, "Z": 0,
            "Name": "Car1"
         },
        "Car2": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": -2, "Z": 0,
            "Name": "Car2"
         },
        "Car3": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": 2, "Z": 0,
            "Name": "Car3"
         },
        "Car4": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": 6, "Z": 0,
            "Name": "Car4"
         }
      }
    }
```            


<br>

■  Single play

- How to change back to one vehicle is created as follows.

Json file sample and description

```json
    {
     "SettingsVersion": 1.2,
     "SimMode": "Car",
     "Algo": {
        "Map": "1"
     },
     "Vehicles": {
        "Car1": {
            "VehicleType": "PhysXCar",
            "X": 0, "Y": 0, "Z": 0,
         }
     }
    }
```            


<br>

### Step3. simultaneous vehicle operation

### ■ How to execute client

1. Java

Run on the IDE tool or

After executing the Command window, run “ java MyCar ” in MyCar.class file location (\MyCar\bot_ java\)

2. Python

Run on the IDE tool or

After executing the Command window, run “ python my_car.py ” in my _ car.py file location ( MyCar bo _ python\)

3. cpp

Run on the IDE tool or

After executing the Command window, execute the MyCar.exe file location (\MyCar\bot_ cpp\ DrivingInterface\ Build\ Release\) “ MyCar.exe ”


<br>

### ■ Multiplay

1. For four people, run the simulator (runsv.bat)

2. Run Client 1 to 4 sequentially.

<img src='./Images/4play_screenshot.jpg'>


<br>

### ■ Single play

1. run.bat

2. Run Client

<img src='./Images/1play_screenshot.jpg'>


<br>

Basic Information about Car and Circuit 
[Basic Information](./Basic_Info_En.md)
