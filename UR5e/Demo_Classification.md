# Demo: Classification_Automate using QR Code

작성자 : 21700469 유진수

본 md 파일은, 딥러닝 모델(QR 코드 리더기)을 활용한 제품의 분류 자동화 공정 구현에 대해 다루고 있습니다.

데모 구현을 위한 사전 환경 설정은, 아래의 링크를 참조하십시오.

- Ubuntu 18.04 설치 : [Click This Link](https://ykkim.gitbook.io/dlip/installation-guide/ubuntu/ubuntu-18.04-installation)
- UR5e 초기 설정 : [Click This Link](https://github.com/Yjinsu/MIP-Robot_Control_using_ROS/tree/main/UR5e)
- QR 코드 리더기 패키지 다운로드 : 
- 컨베이어 벨트 환경 구축 :

<br>

## 공정 개요

물류 산업에서는, QR코드 또는 바코드를 활용하여 물품의 종류를 판별합니다.
또한, 컨베이어 벨트를 활용하여 물품을 이송합니다.

본 프로젝트는 이러한 환경 및 설비로부터 취득한 데이터를 기반으로, 로봇 팔을 제어하는 것을 목적으로 합니다.

해당 목적을 달성하기 위해 설계한 공정의 개요를 대략적으로 표현하면 아래와 같습니다.

<br>

![image](https://user-images.githubusercontent.com/84503980/206390286-cf8e0846-62fd-44e2-9d32-0f4f629fd023.png)

<br>

### **분류 공정 <br>**
컨베이어 벨트를 타고 물품이 운송됩니다. <br>
비전 센서에 4개의 QR 코드가 인식되면 물품이 정상적인 위치에 도달했다고 판단하고, QR 코드의 정보를 로봇에 송신합니다. <br>
이후 수신된 정보를 기반으로, 컨베이어 벨트 좌/우에 놓인 상자에 물품을 분류 적재합니다.

본 프로젝트에서는, A1 & A2 & B1 & B2 라는 정보를 갖는 QR 코드를 생성하였고, <br>
A 상자와 B 상자 안에 물건을 분류 적재하는 방향으로 공정을 설계했습니다. <br>
1과 2를 굳이 나눈 것은, 경우의 수를 늘림으로써 보다 복잡한 공정을 구현하기 위함이었습니다.


<br><br>

## 공정 설계

### Why ROS? <br>

로봇 제어 프로그램의 안전성을 검증하기 위해, 시뮬레이션이 가능한 ROS 환경에서 공정을 설계했습니다.

ROS는 Robot Operating System의 약자로, 로봇 소프트웨어를 개발하기 위한 소프트웨어 프레임워크 오픈소스를 말합니다. <br>

노드 간 메시지 교환 방식을 통해 복잡한 프로그램을 잘게 나눠 공동 개발이 가능하며,  <br>
GUI 도구 모음 rqt, 시각화 도구 Rviz, 3차원 시뮬레이터 Gazebo 등을 지원할 뿐 만 아니라, <br>
다양한 프로그래밍 언어(roscpp = c++, rospy = python 등)를 사용할 수 있다는 강점이 있기 때문에 해당 환경을 채택했습니다. <br>

### 코드 알고리즘 설명 <br>

본 공정의 핵심은 비전 센서로부터 취득한 이미지를 영상처리 기법을 활용하여 정제하고, 이를 통해 로봇에 적절한 명령을 내리는 것입니다.
이번 절에서는, 해당 목적을 수행하기 위해 작성한 프로그램에 대해 설명하고자 합니다. 

<br>

#### 1. Image_Processing.py

카메라로부터 취득한 이미지로부터 QR 코드를 읽어내고, 로봇을 제어하는 노드로 메세지를 보내는 프로그램입니다.

```

```







<br><br>

## 공정 구현

아래의 코드를 순차적으로 copy & paste 함으로써, 손쉽게 공정을 구현할 수 있습니다.

<br>

### 1. 로봇-노트북 연결
```
# Simulation
roslaunch ur_gazebo ur5e_bringup.launch
roslaunch ur5e_sim_moveit_config move_group.launch

# Real
roslaunch ur_robot_driver ur5e_bringup.launch robot_ip:=192.168.0.2
roslaunch ur5e_real_moveit_config move_group.launch
```

<br>

### 2. 이미지 취득
```
# Depth Camera 사용 시 아래 코드 실행
roslaunch realsense2_camera rs_camera.launch align_depth:=true

# 웹캠 사용 시 아래 코드 실행
rosrun usb_cam usb_cam_node
```

<br>

### 3. 이미지 프로세싱
```
# 이미지 내부 QR 코드 인식, 메세지 송신
rosrun ur_interface Image_Processing.py
```

<br>

### 4. 로봇 제어
```
rosrun ur_interface closed_loop_system
```


