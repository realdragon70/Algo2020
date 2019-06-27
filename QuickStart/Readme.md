## 시뮬레이터 설치하기 
### 01. 시뮬레이터 준비하기
--------------------------------

시뮬레이터를 다운받습니다. 시뮬레이터에 맵이 포함되어 있으며, 각 맵별로 시뮬레이터 파일이 배포됩니다.

※ [관련 파일 다운로드 링크](https://drive.google.com/drive/folders/1fkf2ihHAxDxyMN9ABvPnUzwMGZhUcGJm)


시뮬레이터 실행환경은 MS Windows 7 / MS Windows 10 입니다.

다운받은 파일압축을 풀면 다음과 같이 되어있습니다. 이곳에서 Algo.exe 를 실행하면 됩니다.

<img src='./Images/1.png'>
<br>
	  
만약 편의 혹은 PC 성능의 문제로 전체화면이 아니라 작은 화면으로 띄우기를 원하시는 경우 run.bat 를 실행하시기 바랍니다. run.bat 파일에서 화면의 가로 세로 사이즈를 지정할 수 있으며, 첨부된 파일 에서는 -ResX=640 -ResY=480 로 지정되어있습니다.

처음 Algo.exe 파일을 실행하는 경우 UE4 설치를 요구합니다. UE4 Prerequisite 설치 완료 후에, 시뮬레이터가 실행됩니다.

<img src='./Images/2.png'>
<br>

그리고 실행시 다음과 같은 다이얼로그에서 Yes를 선택하여 주시기바랍니다. (No 를 하는 경우 자동차 대신 드론이 나타납니다)

<img src='./Images/3.png'>
<br>
	  
시뮬레이터가 실행된 화면입니다.

<img src='./Images/4.png'>
<br>

시뮬레이터 도움말

- F1 키를 누르면 도움말이 나옵니다.

<img src='./Images/5.png'>
<br>
	  
settings.json 수정하기

- 아래와 같이 수정바랍니다.

Path : C:\Users\SDS\Documents\AirSim

File : settings.json

```

    {
	 "SettingsVersion": 1.2,
	 "SimMode" : "Car",
	 "ClockSpeed": 1
    }
```	


위 내용은 가장 기본 형태의 세팅입니다.

※ Airsim simulator 의 clock speed 에 대하여.

Path : C:\Users\{사용자}\Documents\AirSim 이하에 생성되는 settings.json 을 수정하여, 시뮬레이터의 속도를 조절할 수 있습니다. Airsim 공식문서에서는 clock speed 를 올리면, 물리법칙 왜곡 등, 품질이 떨어질 수 있다고 하고 있습니다. 따라서 서버에서 검증시에는 1배속으로 주행시킬 예정입니다. 로컬에서 테스트 하실때에는 가급적 2배속 이내에서 테스트를 진행해주시기를 권고드리며, 최종제출시에는 1배속에서 검증을 해주시기 바랍니다.



※ Airsim simulator 2 배속 주행으로 수정하기

- setting.json 수정 -> "ClockSpeed": 2
- 룰 주행의 경우 : drive_controller.py 의 최상단에 'current_clock_speed = 2' 로 수정
- 자율 주행의 경우 : dqn_model.py 의 최상단에 'current_clock_speed = 2' 로 수정



### 02. 아나콘다 설치하기

A. 아래의 URL로 접속하여, 3.7 버전 설치 파일을 다운로드 받습니다.

접속하면 macOS가 기본으로 선택되어 있으므로, Windows 메뉴를 선택해 주세요.

<img src='./Images/6.png'>
<br>

https://www.anaconda.com/distribution/#download-section


B. 설치 파일을 실행하여, Anaconda를 설치합니다.

Installation Type은 어느 것을 선택해도 상관없습니다. 여기서는 Just Me를 선택해 봅니다.

ALL Users 를 선택 하여도 무방합니다. 다만, 패키지를 설치 또는 삭제시 cmd 창을에서 관리자 권한을 요구하는 경우가 있습니다.

<img src='./Images/7.png'>
<br>

C. 고급 설치 옵션 선택하기.

<img src='./Images/8.png'>

a) Adding Anaconda to my PATH environment variable (default 는 체크해제)
<br>
다음과 그림과 같이 Path 환경변수에 Anaconda를 추가하는 옵션입니다. 기존에 사용하던 파이썬 실행환경이 Path에 추가되어있는 경우 꼬일 수 있으므로, 이 옵션을 해제합니다.

만약 아나콘다를 처음 설치하는 사용자라면 이 옵션을 체크해도 무방하며, cmd 창에서 현재 디렉토리 위치와 상관없이 파이썬을 실행 할 수 있습니다.

이 모든것을 신경쓰고 싶지 않다면, 체크 해제한 상태로 설치하고 cmd 창 대신에 Anaconda Prompt 를 사용하시면 됩니다.

<img src='./Images/9.png'>

b) Register Anaconda as my default Python 3.7

아나콘다를 기본(Default) 파이썬 실행환경으로 인식시킬지 여부를 선택하는 옵션입니다. 기존에 사용하던 파이썬이 없다면 선택(checked) 상태로 Install 을 하면 됩니다.

여기까지 하면 설치는 진행이 되고, 파일작업이 많아 설치 완료까지 다소 시간이 걸릴 수 있습니다.

설치가 완료되면 command (cmd) 창 혹은 Anaconda prompt 에서 python 버전을 확인해보시기 바랍니다.


다음과 같이 나오면 설치가 정상적으로 이루어진 것입니다.
```
C:\Users\SDS>python --version
  Python 3.7.3 :: Anaconda, Inc.
```

### 03. Airsim 모듈 설치하기

command (cmd) 창 혹은 Anaconda Prompt를 관리자 권한으로 실행 후 아래 명령어를 입력하시기 바랍니다.

(command 창에서 pip install 이 원활하게 진행되지 않는 경우, Anaconda Prompt를 권장합니다.)

프록시 설정은 선택 사항입니다. 개발 환경(사내/사외)에 따라 적절하게 변경하세요.
```
C:\Users\SDS>pip install airsim --proxy 프록시주소:포트 --trusted-host pypi.org
```

※ airsim 설치 도중에 다음과 같은 경고가 나타나지만, 실행에는 문제가 없습니다.

#distributed 1.26.0 has requirement tornado>=5, but you'll have tornado 4.5.3 which is incompatible.

<br>

자 이제 거의 준비를 마쳤습니다.
<br>
[룰기반주행](./Rulebase_Start.md) 또는 [자율주행](./Autonomous_Start.md)으로 이동하여 계속 진행해 주세요.

<br><br>
------------
<br><br>

## Get Simulator
### 01. Getting Airsim simulator ready.
--------------------------------

Please, download the Airsim simulator you want to play. A simulator file has only one map file. You should choose which one to download depending up on the map you want to.

※ [Download link](https://drive.google.com/drive/folders/1fkf2ihHAxDxyMN9ABvPnUzwMGZhUcGJm)


The runtime for Airsim is Microsoft Windows. We have tested on Windows 7, 10

Once you download a zipfile and unzip, they will look like below. You can execute Algo.exe to run Airsim simulator.

<img src='./Images/1.png'>
<br>
	  
If you don't want to run as a full screen for your convenience or performance issue, you can execute run.bat which will run the simulator on a popup window. Its resolution is set 640x480 as a default but you can customize it on your convenience by editing run.bat.

The very first time you executing the Algo.exe file, it will request you to install UE4 Prerequisites. Once it is done, simulator will automatically come up.


<img src='./Images/2.png'>
<br>

And please select 'Yes' to the following dialogue. (If 'No', then a drone mode will be activated)

<img src='./Images/3.png'>
<br>
	  
Vehicle simulator is now running like a screen.

<img src='./Images/4.png'>
<br>

Simulator Help

- Press F1 for help.

<img src='./Images/5.png'>
<br>
	  
Modifying settings.json

- modify as follows.

Path : C:\Users\SDS\Documents\AirSim

File : settings.json

```

    {
	 "SettingsVersion": 1.2,
	 "SimMode" : "Car",
	 "ClockSpeed": 1
    }
```	

The above is the default setting.

※ About clock speed of Airsim simulator

By modifying settings.json file in the path : C:\Users\{username}\Documents\AirSim, you can change the speed of Airsim simulator. The Airsim official document said by increasing clock speed may deteriorates simulator quality, such as physical law distortion. Therefore, when code/model is submitted, the server will run the code/model with x1 speed. When testing locally, we recommend that you run the test within 2x and for the final submission, please verify in the x1 speed environment


※ Modifying to x2 speed environment

- Edit setting.json -> "ClockSpeed": 2
- Rule based driving : At the top of drive_controller.py file, modify 'current_clock_speed = 2'
- Autonomous driving : At the top of dqn_model.py file, modify 'current_clock_speed = 2'



### 02. Installing Anaconda

A. Please, retrieve the latest version(3.7) of Anaconda fro the URL below.

MacOS is selected by default, so choose the Windows menu.

<img src='./Images/6.png'>
<br>

https://www.anaconda.com/distribution/#download-section


B. Run the installation file and move on step by step by clicking the next button.

There are two Installation types. 'Just me' is chosen for now.

'All Users' option is also OK. But it requires admin privileges whenever you install packages or modifying configuration of Anaconda.

To give admin privilege, find the program you want to run - in this case command prompt(cmd) - right click and select 'Run as administrator'.


<img src='./Images/7.png'>
<br>

C. Select advanced installation options


<img src='./Images/8.png'>

a) Adding Anaconda to my PATH environment variable (default is unchecked)

This option will add Anaconda path to the environment variables. If you have previously installed python runtime, you can uncheck this option. And if you are installing Anaconda for the first time in your PC, you can check and proceed. This will allow for you to execute python at any directory location. Id don't want to think about these, you can just uncheck it and use Anaconda prompt instead of cmd prompt.


<img src='./Images/9.png'>

b) Register Anaconda as my default Python 3.7

this option will set Anaconda as a default Python runtime. If you don't have it previously, check and continue to install.

After you select all the choices, the complete installation process will take some times. Please be patient.

Once installation is done, run cmd command or Anaconda prompt from start menu and check python version by typing this command.



If you see current version information like this, it is considered the installation is properly done.
```
C:\Users\SDS>python --version
  Python 3.7.3 :: Anaconda, Inc.
```

### 03. Installing airsim module

Run command below on cmd or Anaconda prompt (with administrator privilege)

(Anaconda prompt is recommended if the pip install fails in the command window.)

Proxy settings are optional. Make the appropriate changes according to your environment.

```
C:\Users\SDS>pip install airsim --proxy 프록시주소:포트 --trusted-host pypi.org
```

※ while airsim package installation, you can encounter a warning message but it doesn't affect the function that we are going to use.

#distributed 1.26.0 has requirement tornado>=5, but you'll have tornado 4.5.3 which is incompatible.

<br>

We are almost ready.
<br>
Go to Rule-based Driving or Autonomous Driving to continue.
Go to [Rule-based Driving](./Rulebase_Start_Eng.md) or [Autonomous Driving](./Autonomous_Start_Eng.md) to continue.
