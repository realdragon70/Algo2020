Hello?

We've got a lot of questions via email and other channels and are answering it.
We will continue to make announcements so that you can refer to subsidiaries 
and overseas corporations.

---------------------

Q. Are there any restrictions on the driving_clinet.py file?
Are there any restrictions on importing other modules like import math or 
declaring classes other than DrivingClinet inside?

A. It's possible to add class declaration, method, etc. in the file.
You can freely work within one file that you submit.


Q. When I was driving, I thought I would like to have more maps to actually test.
I was going to make the map myself, but I heard that many of the plugin and
other things have been modified and distributed.
If so, how many more additional plans do you plan to provide, and if so, how?
Please let us know briefly. If you have a way to test it myself.

A. Currently, only two maps are available, BasicRound and SpeedRacer.
For now, We'll proceed with the following schedule.
SpeedRacer hurdle version(with many obstacles) will be released around 6 pm(KST) on July 8.
Smurf valley map will be released at 6 pm(KST) on July 9.
We'll notify when a new schedule comes out for maps that will be released later.


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

Q There is no brake action in autonomous driving model. Can I put a brake action on it?
A. No problem, You can use it. However, when we tested it, It's not working properly.

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

Q. I felt that it is not easy to learn as the width of the road track changed in autonomous driving.
    Please let me know which width is actually used or fixed?
A. Currently, the road width is 16M, which is mostly set.
    However, we provide variable that specify the width of the road, Please refer to it.
    # road half width + car half width
      self.half_road_limit

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

Q.  I have been having trouble working with the autonomous training process. 
    If I set clock speed to 2 (in both the settings file and the model.py file), and then I run dqn_custom_client.py, 
    to train the program trains once, and then for every subsequent step it doesn’t even drive and just refreshes. 
    In the game, the car just continually resets to the starting position every second and doesn’t do anything. 
    If I change the clock speed to 1 it runs fine, but if it is set to 2 then it does not work. What could I be doing wrong?
A. For the autonomous driving, there's a code block that let the vehicle drive straight for a couple of second at the beginning 
    but I think it is affected by clock speed and pc specification. I will find the way to correct that and patch the source later. 
    For now you can try to modify this part and let us know if it works.

==== dqn_model.py =================================
381 line - get rid of yellow block 
def is_done(self, car_state, prev_car_state, reward, frozen=0):
    done = 0
    if reward <= -1:
        done = 1
    elif car_state.speed <= 1:
        done = 1

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

Q. Smurf maps are different from speed racing map, because of road characteristics, driving performance is different.
    If this is different for each map, Shall we submit different codes for each map when submission?
A. It is not particularly different from a Smurf map. There seems to be a difference in the amount of resources rendered maps. 
    And, in the qualifications and tournaments, instead of submitting different codes for each map, 
    you run multiple maps with only one source code. In other words, 
    you have to submit a source that runs well throughout the various tracks.

Q. In the autonomous driving, I want to give the reward by looking at the time 
    when sensing_info.lap_progress exceeds 10%, 20%, and 30%.
    In this regard, we want to declare and initialize member variables

    1) Where can I define member variables?
    2) Where can I initialize variables when I start a new lap?

    I want to use member variables in the def comput_reward function. 
    If set it Inside this function, It is initialized every time when it is executed.

    For example:
    Where can I declare finish10 and cnt when I start lap?

def compute_reward 
cnt=cnt+1
if sensing_info.lap_progress > 10 and finish10 = False :
    finish10 = True
    reward = reward+cnt/1000
    cnt = 0

A. Declare the variable outside the method as follows, and access it by using self in the method.
    Initialize it, when Reward is -1.

#member variables
variable_count= 0
variable_bool= False

# =========================================================== #
# Reward Function
# =========================================================== #
def compute_reward(self, sensing_info):

    # =========================================================== #
    # Area for writing code
    # =========================================================== #
    # Editing area starts from here
    #
    thresh_dist = self.half_road_limit  # 4 wheels off the track
    dist = abs(sensing_info.to_middle)
    reward = 0

    # ...some codes

    if self.variable_bool == False :
        #do something
        self.variable_count = self.variable_count+ 1


    # when reward -1 -> reset variables
    if reward == - 1 :
        self.variable_count = 0
    #
    # Editing area ends
    # ==========================================================#
    return reward


Q. Are we supposed to use different model weight for each track given for evaluation?
A. Yes, you can use different model weight for each track. There will be competitions within each map.
    But also for the final competition, we are planning to get submission for general model which runs several tracks well. 
    In that case, you should train the model with several tracks. Those tracks will be noticed prior to the final competition.

Q. Can I submit the learned model multiple times to check the result until the final submission date or once you submit it will the final?
A. Yes, you can submit as many times as you want to evaluate you model on the server. 
    The lap time can be differ from local machine because of different condition (CPU, RAM) 
    but we are on the process of unifying the specification of the server machines 
    and will be finished within this week to make fair condition among participants.



