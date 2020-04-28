[Korean](./README.md) | English

## Introduction  
------------------------
Algorithm Contest is a car race using vehicle simulator(Microsoft Airsim), which is a competition in which several vehicles compete with the 3D modeled racing track through the driving time or the competition.

By directly creating an algorithm corresponding to each state of the vehicle, It is the secret to be the champion by developing the optimal driving algorithm by utilizing various APIs that provide information such as the status, location information, speed and direction of the road where the vehicle is running in real time.

The race is a way for two vehicles to compete against the winner and proceed to the preliminary (league) and finals (tournament). The preliminaries are performed by measuring the record by single play per track and ranking. In the final round, two cars will compete one-on-one, and the winner will advance to the next round and pick the final winner.


### The detailed information about the contest

All teams will compete in the qualifying league, and the top eight teams will advance to the finals with single runs on the road chosen as the qualifying track.

We will choose the winner through online preliminaries and offline finals.


### On-line Qualification (8 teams will be selected)

The preliminary round will be held in a single league with no separate group, and will proceed with the following rules.

The qualifying track will be announced by notice after your learning and bot-development tests have been fully conducted.

  - The qualifying score is determined by the total time taken from the starting line to the finish line and two laps.
  - Replicating the source code of another team, or submitting it utilizing a similar code, may be disqualified.
  - Team configurations can be organized freely regardless of area and division, and can consist of 1 to 3 people.
  - In order of grades from 1st to 8th place, the qualifying team is selected, but if there is a tie, all the lower equalizer teams pass the qualifying round.


### Off-line Main Event 

From the 8th round, the final winner will be selected by the tournament. The loser is eliminated, the winner goes to the next round, and the winner of the last two teams is the winner. If both teams are disqualified, the longer the driving distance will win. The starting position of the two teams is that the team that scored better in the preliminaries or the previous match will start from the inside or the front.


### Disqualification Standards

### ■ Contest rule(Disqualification)

- If you do not return to the track after departing from the designated track and take advantage of shortcuts or map errors, you will be disqualified.

- If you can not finish within 10 mins after the start of the race, you will be disqualified.

- If the BOT loose the control within 100 mSec or a functional error occurs, you will be disqualified.

- If you pass the checkpoint of the track in an abnormal way, you will be disqualified

- The ‘self.half_road_limit’ is the only variable allowed to use among the variables defined in the parent class. Other variables, including the ‘self.way_points’ and ‘self.all_obstacles’, are not allowed to copy values to local variables manually or access them directly.

- Overriding methods in parent class, especially ‘run()’ method, is not allowed.

- Any illegal acts caused by cheating on simulator or environment setting change will be disqualified. (If you want to use other Apis and development method not defined your own (not built-in API), Please be sure to ask the Contest TF in advance).

- After the game, if any cheating is found through a post review (We will check the video and source code), the result will be canceled.



### ■ Contest rule (re-competition)

If a car cannot be operated due to a collision between vehicles while racing, a re-competition will be held.

-The cases that are not correspond to a collision with the opponent are excluded. For example, an overturn when cornering, collision with obstacles or other feature, etc.

- If a car turns upside down and rotates 360 degrees and returns to a state that driving is possible, it is not the case for re-competition

- Re-competition limit is 3 times. If it continues to run out of control, the team that goes a little farther from the last attempt will win.

- If a car hit into a fence or obstacles, it is not the case for re-competition becuase you can go backward and continue driving.


### ■ Other rules

- The tracks for qualification/Main eventis will be selected by the contest TF

- The operating rule of the competition can be changed according to circumstances and will be announced prior to change.

<br>
Ok! Let's go to start develop this game! 

[QuickStart](./QuickStart/Readme_Eng.md)

Basic Information about Car and Circuit 

[Basic Information](./Guide/Basic_Info_En.md)


Autonomous driving guide has been added.

[Additional Autonomous driving guide](./Guide/Auto_Guide_Advanced_Eng.md)
