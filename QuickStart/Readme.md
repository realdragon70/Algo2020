Korean | [English](./Readme_Eng.md)  | [Home](../README.md)

## 시뮬레이터 설치하기 
### 01. 시뮬레이터 준비하기
--------------------------------

시뮬레이터를 다운받습니다. 시뮬레이터에 트랙이 포함되어 있으며, 각 트랙별로 시뮬레이터 파일이 배포됩니다.

※ [관련 파일 다운로드 링크](https://drive.google.com/drive/folders/1aB7uDYu3Maf3zcMCYBuEb7HRT0RCxNXt?usp=sharing)


시뮬레이터 실행환경은 MS Windows 7 / MS Windows 10 입니다. (64 bit)

다운받은 파일압축을 풀면 다음과 같이 되어있습니다. 이곳에서 run.bat 를 실행하면 됩니다.

<img src='./Images/sim_install_guide_1.jpg'>
<br>
	  
만약 편의 혹은 PC 성능의 문제로 전체화면이 아니라 작은 화면으로 띄우기를 원하시는 경우 run.bat 를 실행하시기 바랍니다. run.bat 파일에서 화면의 가로 세로 사이즈를 지정할 수 있으며, 첨부된 파일 에서는 -ResX=640 -ResY=480 로 지정되어있습니다.

처음 Algo.exe 파일을 실행하는 경우 UE4 설치를 요구합니다. UE4 Prerequisite 설치 완료 후에, 시뮬레이터가 실행됩니다.

<img src='./Images/2.png'>
<br>

그리고 실행시 다음과 같은 다이얼로그에서 Yes를 선택하여 주시기바랍니다. (No 를 하는 경우 자동차 대신 드론이 나타납니다)

<img src='./Images/3.png'>
<br>
	  
시뮬레이터가 실행된 첫 화면입니다.

<img src='./Images/sim_install_guide_2.jpg'>

1. 닫기, 최대화 등 윈도우 창 기본 동작을 통해, 시뮬레이터를 종료하거나, 최대화할 수 있습니다.

2. 보안 안내 문구 입니다.

Simulator 반복 실행 중, 이상 동작 발생 시, 작업관리자 들어가서, algo-win64-Shipping.exe 강제 종료 후, 재시작을 실행해 봅니다.


<br>

시뮬레이터 도움말

- F1 키를 누르면 도움말이 나옵니다.

<img src='./Images/sim_install_guide_3.jpg'>

단축키를 통해 기능을 제공하고 있습니다.

1. F8 : 키보드를 통해서 조정 가능한 수동 모드로 시작됩니다.

2. Backspace : 시뮬레이터 초기화. 주행 시도 후, 다시 시도하고 싶은 때, 활용합니다.

3. 카메라 수동 조정 : 상세 내용은 도움말 참조

4. 카메라뷰 조정
- F : FPV view, B : “fly with me” view, \ : ground observer view, / : chase with spring arm view

시뮬레이터의 주행화면입니다.

<img src='./Images/sim_install_guide_4.jpg'>

1. 미니맵으로 트랙상의 위치를 나타냅니다.

2. 현재 Lap / 전체 Lap 수

3. 주행시간

4. 기어

5. 속도 (km/h)

주행 완료 후, 혹은 중단하고 다시 진행을 원할 때에는 "backspace" 키를 통해 초기화 후 진행합니다.


<br>
	  
### 02. 설정 파일 수정하기

settings.json 수정하기

Path : C:\Users\{사용자계정명, 예 -> SDS }\Documents\AirSim

File : settings.json

```

    {
	 "SettingsVersion": 1.2,
	 "SimMode" : "Car"
    }
```	

위 내용은 가장 기본 형태의 설정입니다.

아래 내용은 설정이 가능한 내용들입니다.

settings.json을 수정 후에는 simulator를 재실행해야 합니다.

“Map”의 경우, 장애물 구성 종류를 나타내며,

“Map”는 "1", "2" or "3" 중 한 값을 가질 수 있습니다.

정의가 되지 않는다면, 1에서 3 장애물 중 임의로 하나 설정됩니다.

```
    {
	 "SettingsVersion": 1.2,
	 "SimMode" : "Car",
	 "Algo": {
	 	"Map": "1"
	 },
	 "Vehicles": {
	 	"Car1": {
			"VehicleType": "PhysXCar",
			"X": 0, "Y": 0, "Z": 0
		}
	 }
    }
```	


<br>
	  
### 03. 키보드 모드 사용해서 주행해보기

키보드 모드 사용하기

시뮬레이터 실행 후 "F8" 키 입력 (방향키로 자동차 조작 가능합니다)

※ Client Python 실행 이후에는 "F8" 키 입력이 불가능하며, “backspace”키로 시뮬레이터 초기화 후 다시 가능합니다.

이제 거의 모든 준비를 마쳤습니다.

게시판의 상세 가이드를 통해, 소스코드를 작성 후 주행을 수행해 보기 바랍니다.

<br>
