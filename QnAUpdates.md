Hello?

We've got a lot of questions via email and other channels and are answering it.
We will continue to make announcements so that you can refer to subsidiaries 
and overseas corporations.

---------------------

Q. Are there any restrictions on the my_car.py file?
Are there any restrictions on importing other modules like import math or 
declaring classes other than DrivingClinet inside?

A. It's possible to add class declaration, method, etc. in the file.
You can freely work within one file that you submit.


Q. When I was driving, I thought I would like to have more maps to actually test.
I was going to make the map myself, but I heard that many of the plugin and
other things have been modified and distributed.
If so, how many more additional plans do you plan to provide, and if so, how?
Please let us know briefly. If you have a way to test it myself.

A. Currently, about 6 maps.

Q. When I race with opponent team, We will start from the same spot.
How is the left and right(inside or outside) position determined?

A. As you know, We have a rule to determine start position.
Regarding starting point, inside position will be given to the team who gets better result from the previous match. 

Q. I modified setting.json for a multiplayer game, and when I run Algo.exe, 
It's rolled back to previous file(.json) and only one car is displayed in the simulator.
I can't test a two-player game. Is there any solution to solve this problem?

A. This issue is an encoding issue that occurs because the PC name is not in English,
and Airsim now allows only the path to save and load json in Korean.

The solution is as follows

1. Enter My Computer.
2. Crease 'SDS' folder on drive C (root)
3. Click Library on the left - Documents
4. Click Right buttion on My Documents, and Click Properties 
5. Click the location tab
6. input 'C:\SDS\ in the box and confirm.

If there is a problem after the above change and after the contest,
You can roll it back.

Q. I can give the steering value from -1 to 1, I want to know the actual angle according to the steering value (When steering value is 1)

A. As a result of checking the property value of the vehicle, the angle when steering value is 1 is 50 degree.


Q, When I start, I start after 3 seconds countdown, and I want to know when the car accelerates.
    I wonder if the accelerator is being pressed from the countdown, or whether accelerator is pressed after 1 is counted.

A. It has been developed to apply accelerator values from the moment when 1 disappears and GO is displayed.


Q. How is the handling of the opponent vehicle obstructing the running from the front with the emergency brakes?

A. Intentional braking may be disqualified for the purpose of overturning the opponent vehicle rather than the normal driving.
    The website competition rule (disqualification processing) part also stipulates as follows.
   - If you make the other team's vehicle impossible to operate or drive, you will be disqualified.
    However, normal frontal obstruction is allowed and collision and bump are allowed 
    if you do not cause the opponent vehicle's failure or overturning


Q. Is it possible to import the following parts needed for development?
    import math from scipy
    import interpolate
    
A. Most packages are importable. When adding packages that are not Anaconda native packages,
We'll also install it on the server and provide the environment for importing.


Q. Will a new map(track) be added during the tournament? 
    Or is the map specified and randomly selected?
    
A. As it is known, new maps will be released continuously before the competition.
    In the preliminary league, two maps were selected, and the race is run on any of these maps randomly.
    In the preliminary and final games, we will user several maps.
    (Please check the announcement for details, Notice - Schedule menu on the homepage)


Q. For the rule-based competition, are we writing a different algorithm for every single map to get the fastest time, 
    or are we submitting one algorithm that will be used for all maps? 
    In either case, in the competition, will the algorithms be tested on new maps, 
    or will they only be tested on maps that have been released? 
    The current records from Korea look like they have been written exactly for the maps. 
    I am not sure whether I want to write code that designs a car that can run well even on a map 
    it has never seen before, or if I simply want to optimize my vehicle to be the fastest on the maps that you have presented to us
    
A. The competition will be made among the map that are release (A few more maps are on the way to release, soon).
    For the leader board, It seems like they are writing the code for the specific track. 
    but the real competition will not be on just one single map. and also it will be a match with 2 car racing. 
    So, there will be more accidental factors. Ultimately, the algorithm should be working well for the various map 
    and also responsive to unexpected situation.
    Regarding competition rule and how to will be announced today. So please check with that.


Q. Even if I run the same source code on the simulator, the lap time is about twice as slow on my PC.
    It seems that the performance of the PC is likely to be affected, 
    but is there anything that needs to be checked because there are too many differences?
A. Delays may occur between the simulator and the program depending on the user environment.
    This will affect the running speed and time measurement. This may cause a difference.
    The same PC may have a large difference depending on resource usages on PC.
    Therefore, the tournament simulator PCs are kept fairly equally with the same specifications and conditions.


Q. When Prior to departure counting, sensing_info.moving_forward is sometimes returned as False.
    I think it must be True in this circumstances.
A. The current sensing_info.moving_forward value is implemented as follows.

1. Use the current waypoint and the next waypoint to create an angle by finding the angle you need to move.
2. Obtain the current vehicle's travel angle using the previous 
   (0.1 second before) coordinates of the vehicle, the coordinates of the current vehicle and the above criteria.
    ex) If the reference angle and the vehicle's moving angle are the same, the value is 0

It calculates the angle at which the vehicle is moving and returns the value according to the following conditions.
if -90 < my angle < 90, return True.
To be clear, it is False if it is away from the destination and True if it is getting closer.


Q. Can I turn off the mouse capture option in the simulator's Unreal Engine? I want to switch to Alt + tab.

A. (Thanks to Google for finding your answer.
    Fixed some options in the project settings in the Unreal Engine.    
    We will apply it to the next version of the patch distribution.
    

Q. You said that you are going to the tournament through 1 vs 1 from the rule based race preliminaries.
    Whether this is the left or right of the vehicle position is very important.
    Is there a solution to the problem where the position of the vehicle can determine the win or loss?

A. It is true that the game has an effect on the initial starting position of the vehicle.
    It is advantageous to occupy the inside cornering rather than the obstacle position.
    Considering that, we will place a vehicle based on previous matches and records.
    A variety of situations are expected to occur through friendly matches 
    and various examples of goodwill matches. We'll review and review the guideline.
    

Q. A real car does not slow down so much when I turn off accelerator, but the simulator slows down. Why is this?

A. We didn't make any special setting changes, but it is just the characteristics of the simulator.
