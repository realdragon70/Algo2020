[Korean](./README.md) | English

## Introduction  
------------------------
Algorithm Contest started in a department is now became a big event for employees from subsidiaries and overseas subsidiaries this year.

This event is conducted as a car race using vehicle simulator(Microsoft Airsim) and it's divided into two categories: rule-based driving and autonomous driving

In the rule-based driving, the vehicle get actions directly from the algorithm code corresponding to each state of the vehicle, and for the autonomous driving part, a model trained with proper reward function drives the vehicle.


### The detailed information about the rule based driving



The Qualification consists of eight groups, and the top four teams of each group advance to the 32nd tournament according to their result.

The final winners will be selected through online qualification and offline finals.



### On-line Qualification (32 teams selected)

The teams will play in the league and scores will be awarded according to the race result. The top four teams will advance to the 32nd Division. The win or loss is decided by the lap time of the race that the two team completed the two laps, starting from the same starting point. If both team fails to finish, they will be withdrawn and if they are ranked in the tie, the team who raced longer distance will have the priority. And if there is an error in the BOT on the inpection, the team will be disqualified.

We organize the group according to the company / division unit.

- The league group is organized considering the divisional balance of the participants. It is planned to be composed of approximately 8 teams (composition of group / number of teams can be changed depending on participation status)
- Business divisions with a small number of employees can be grouped with other divisions.


### Off-line Main Event (Top 16 teams will be awarded)

From the 32nd, the tournament match begins. The winner advances to the next round. If both teams fail to finish, the team who raced longer distance will win. Regarding starting point, inside position will be given to the team who gets better result from the previous match. Awards and prizes will be awarded to top 16 teams, they must participate in the tournament and awards ceremony.



### How to organize the match

- The teams who ranked high in the group have match with the teams who ranked low in the pother group.(ex: 1st place team in group A will have match with 4th place team in group B, 2nd place team in gruop 2 wil have match with 3rd place team in group A)






### The detailed information about the autonomous driving




### ■ Online Qualification (collects records by each track)

Unlike the rule based driving, it's not competition between users. Instead, we measure the lap time of each team and show rankings on the leader board. If you submit your model by selecting the track, server will run, measure the lap time and the result will be shown on the homepage automatically.

The rest of the track will be opened one by one and the racing records can be submitted until the main event begins. After the deadline, the teams who has the best record will be awarded.




### ■ Online Main event (collects records across multiple tracks)

For the main event, the goal for the paticipants is to create model which is well trained to race not just one specific track but across multiple tracks. The final winner will be decided by overall score running 2 or 3 tracks selected during the main event period.




### Disqualification Standards



### ■ Contest rule (Disqualification)

- If you do not return to the track after departing from the designated track and take advantage of shortcuts or map errors, you will be disqualified.

- If you can not finish within 10 mins after the start of the race, you will be disqualified.

- If the BOT loose the control within 100 mSec or a functional error occurs, you will be disqualified.

- If you pass the checkpoint of the track in an abnormal way, you will be disqualified

- If you make the other team's vehicle impossible to operate or drive, you will be disqualified.However, normal frontal obstruction is allowed and collision and bump are allowed if you do not cause the opponent vehicle's failure or overturning

- Any illegal acts caused by cheating on simulator or environment setting change will be disqualified. (If you want to use other Apis and development method not defined your own (not built-in API), Please be sure to ask the Contest TF in advance).

- After the game, if any cheating is found through a post review (We will check the video and source code), the result will be canceled.



### ■ Other rules

- The tracks for qualification/Main eventis will be selected by the contest TF

- The operating rule of the competition can be changed according to circumstances and will be announced prior to change.

<br>
Ok! Let's go to start develop this game! 

[QuickStart](./QuickStart/Readme_Eng.md)
