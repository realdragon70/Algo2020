Korean | [English](./README_Eng.md)

## 대회소개 
------------------------

알고리즘 경진대회는 차량 운행 시뮬레이터(Microsoft Airsim)를 활용한 자동차 레이스로, 3D로 모델링된 경주 트랙을 여러대의 차량이 주행시간 혹은 대전 경기를 통해 성적을 겨루는 대회입니다. 

차량의 각 상태에 대응하는 알고리즘을 직접 작성함으로써 차량을 주행시키며, 차량이 달리고 있는 도로의 상태, 위치 정보, 속도와 방향 등의 정보를 실시간으로 제공하는 여러 API를 활용해 최적의 주행 알고리즘을 개발하는 것이 우승으로 가는 비결입니다. 

경주는 여러대의 차량이 대전을 하여 승자를 가리는 방식이며, 예선 및 본선으로 진행됩니다. 예선은 트랙별 기록을 측정하고, ranking 을 매기는 방식으로 진행합니다. 본선에서는 여러대의 차량이 대결을 벌여 상위를 차지한 팀이 다음 라운드로 진출하고, 최종 우승자를 가려낼 예정입니다.



### 대회 진행 상세 안내


예선 리그전은 모든 참가팀이 성적을 겨루게 되며, 예선 주행 트랙으로 선정된 도로를 달려 주행 성적으로 상위 8개팀이 본선에 진출합니다.

온라인 예선과 오프라인 본선을 통해 최종우승자를 가립니다.



### ■ 온라인 예선 (8개팀 선정)

예선은 별도의 조편성 없이 참가자 전원이 단일 리그로 성적으로 우위를 가리며, 다음의 규칙으로 진행합니다.

- 예선 경기 대상이 되는 주행 트랙은 여러분의 학습과 봇개발 테스트가 충분히 이뤄진 후 공지를 통해 공개합니다.
- 예선 성적은 출발선에서 시작하여 결승점을 통과하여 2바퀴를 돌았을 때의 시간 합계로 결정됩니다.
- 다른 팀의 소스코드를 복제하거나, 유사코드를 활용하여 제출하는 경우 실격처리 될 수 있습니다.
- 팀 구성은 자유롭게 구성할 수 있으며, 1~3인까지 구성 가능합니다.
- 1위~8위까지 성적순으로 예선 통과팀을 선정하지만, 동점인 경우가 발생할 경우에는 하위 동점기록팀 모두 예선을 통과합니다.


### ■ 오프라인 본선 (8강 토너먼트)

8강부터는 토너먼트 대전 방식으로 최종 우승자를 선정합니다. 패자는 탈락하고, 승자는 다음 라운드에 진출하여, 최후에 남는 두 팀의 승자가 우승자가 됩니다. 두 팀이 모두 실격할 경우, 주행거리가 더 긴 쪽이 승리하는 것으로 합니다. 두 팀의 출발 위치는 임의 방식으로 정해집니다. (랜덤하게 차량 배치)


### 대진 구성 방식

- 대진 구성은 추첨을 통해 랜덤하게 이뤄지며, 해당 대진에 따라 우승팀을 가립니다.  
  (대진 추첨은 공정한 방식을 통해 여러분에게 공지되도록 할 예정입니다.)
- 예선 통과팀이 8팀 이상으로 부전승이 발생할 경우에는 성적순으로 상위팀에게 부전승의 특전이 주어집니다.



### 대회 실격 처리 기준

### ■ 대회 규칙 (실격 처리)

- 정해진 트랙(도로)에서 이탈 후 지속적으로 복귀하지 않는 경우, 지름길이나 지도 오류 활용시 실격 처리

- 경주 시작 후, 일정시간 (10 min) 이내 완주하지 못하는 경우. 주행을 완료할 수 없는 상태에 도달한 경우도 포함합니다. (차량 전복, 장애물로 인한 주행 불가 등)

- 주행 BOT이 일정시간 (100 millisecond) 이내에 주행 제어를 하지 않는 경우, 기능 오류가 발생하여 정지한 경우

- 주행 트랙의 체크포인트를 비정상적인 방법으로 통과하여 주행하는 경우

- self.half_road_limit 외에 부모에 선언된 변수의 값에 접근할 수 없습니다. 이 밖에 self.way_points, self.all_obstacles 를 비롯한 여타 변수에 대해서는, 직접 접근하거나 미리 값을 로컬 변수에 저장해두고 사용하는 방식을 허용하지 않습니다.

- run() 함수를 포함하여 부모의 메소드를 override 하는 것을 허용하지 않습니다.

- 시뮬레이터 조작이나 정하지 않은 주행 환경 설정 변경으로 인한 부정행위 (정해진 주행환경 설정과 기본 제공 API 이외의 개발 방법 적용 시 반드시 대회운영TF에 사전 확인바랍니다.)

- 경기 이후에라도 사후 검토(주행 영상 및 소스코드 확인)를 통해 부정행위가 발견될 경우, 성적은 취소처리 됩니다.



### ■ 대회 규칙 (재 경기)

주행중에 차량 간의 충돌로 인하여 한 차라도 전복거나 더 이상 차량 운행이 불가능하게 되는 경우에는 재경기를 실시합니다.

- 상대방과의 충돌이 아니라 혼자서 주행하다가 코너에서 전복되거나 주행불가 상태로 빠진 경우는 해당하지 않습니다.

- 차가 뒤집혔으나 360도 회전하여 주행이 가능한 상태로 돌아온 경우는 재경기 대상이 아닙니다.

- 3회까지 재경기를 시도해도 계속해서 주행불능 상태에 빠지는 경우, 마지막 시도에서 좀더 멀리 가는 팀이 이기는 것으로 합니다.

- 펜스나 장애물에 부딪힌 경우는, 후진을 통해 주행을 이어나갈 수 있기 때문에 주행불능이라고 판단하지 않습니다.



### ■ 그 외 규칙

- 예선 트랙/본선 트랙은 대회운영 TF에서 지정합니다.

- 대회 운영 방식은 사정에 따라 변경될 수 있으며, 변경 전 충분히 사전 공지를 할 예정입니다.

<br><br>
자, 그럼 설치하러 가보실까요? [QuickStart](./QuickStart/Readme.md)

차량 및 트랙 관련 기본정보 확인은 여기로 [Basic Information](./Guide/Basic_Info.md)

