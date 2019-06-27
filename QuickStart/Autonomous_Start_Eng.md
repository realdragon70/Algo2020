## Autonomous Driving 

### 01. Prerequisites

Pease, follow the steps in the [Get Simulator](./Readme.md)


### 02. Package installation with pip

Once you finish steps above, the following step is to install frameworks for reinforcement learning.

We will install Tensorflow and Keras for the vehicle training.

Please, run the following commands from cmd or Conda prompt. (Cmd window or Anaconda prompt should have administrator privilege unless you chose 'Just me' when you were installing the Anaconda)

Proxy settings are optional. Make the appropriate changes according to your environment.

```bash
#Tensorflow Installation
> pip install tensorflow --proxy 70.10.15.10:8080 --trusted-host pypi.org
        
#Keras Installation
> pip install keras --proxy 70.10.15.10:8080 --trusted-host pypi.org
        
#airsim Installation
> pip install airsim --proxy 70.10.15.10:8080 --trusted-host pypi.org
```     

※ While airsim package installation, you may encounter a warning messages 'distributed 1.26.0 has requirement tornado>=5, but you'll have tornado 4.5.3 which is incompatible.' but it doesn't affect functionality that we are going to use.


### 03. Executing the source code.

Please download source code from the download page.

If you unzipped the downloaded file, they will look like this.

<img src='./Images/10.png'>


Please make sure Airsim simulator is running first, and then run this command.
```bash
> python dqn_custom_client.py
```

If you open the 'dqn_custom_client.py' file, hyper-parameters, action space and reward function are written as a default. Just try it run with tutorial map and start your training !!

```python
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
# weight load option
# =========================================================== #
model_load = False
model_weight_path = "./save_model/ ... /dqn_weight_00.h5"


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
            dict(throttle=0.7, steering=0.1),
            dict(throttle=0.7, steering=-0.1),
            dict(throttle=0.7, steering=0.2),
            dict(throttle=0.7, steering=-0.2),
            dict(throttle=0.7, steering=0)
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
        thresh_dist = 6.5  # 4 wheels off the track
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

For more information, please refer to the [detailed guide](./Autonomous_Detail_Eng.md)
