# MIP-Robot_Control_using_ROS

## Introduction

이 Repository는 한동대학교 2022년 2학기에 진행된 기전융합설계, <br>
**Simulation Environment Establishment for Robot Arm Control** 에 대한 설치 파일 및 튜토리얼이 포함되어 있습니다.


<br>

스마트팩토리의 한 공정에 대한 산업로봇의 제어 코드를 작성하고, 


작성된 코드를 Gazebo에서 안정성 테스트를 거친 후 실제 로봇에 적용하는 시뮬레이션 환경을 구축하는 것이 목적이었습니다. 시뮬레이션 테스트 및 실제 구현해본 공정은 자동 분류 공정입니다.

매니퓰레이터 모델은 **INDY-10 (Neuromeka)**로 로봇 제어를 위한 Linux - ROS를 사용했으며, ROS의 Rviz와 Gazebo 프로그램으로 프로젝트를 진행했습니다.

Rviz는 로봇의 상태를 시각화해주거나, 움직임을 제어하는데 도움을 주는 Move-it 등을 제공해주는 툴입니다.

Gazebo는 로봇의 물리 정보 및 외형 모델파일로 로봇을 가상의 공간에 만들어 움직임 및 제어 등을 테스트 할 수 있는 시뮬레이터입니다.

로봇뿐만 아니라, 사용한 그리퍼 EGP-64 및 Point Grey 카메라에 대한 연결 및 사용법 또한 Repository에 포함되어 있습니다.

**본 프로젝트는 한동대학교 김영근 교수님의 지도아래 진행되었습니다**

Requirements
ROS를 사용하기 위해 Linux- ubuntu 18.04 버전이 필요합니다.

또한 WIFI 연결이 가능한 노트북 or 데스크탑이여야 하며, 이 프로젝트에서 사용한 노트북의 사양은 CPU - Intel i5-1135G7, RAM - 16GB, Graphic card - MX450 입니다. 참고로 윈도우와 리눅스 듀얼 부팅 환경에서 프로젝트를 진행했는데 문제는 없었습니다.

INDY-10 전용 태블릿은 로봇 연결 및 상태 확인과 간단한 제어에 유용함으로 실험할 때 같이 사용하시면 좋습니다.

ROS에서 사용된 코드들은 대부분 **C++**로 작성되었음으로, C++을 잘 다룰수록 수월해집니다.

ROS는 Linux에서 Python 2 버전으로 작동됩니다. Linux의 기본 프로그램이 Python 3버전일 경우 작동되지 않습니다.
