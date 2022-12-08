# Demo: Classification_Automate using QR Code

작성자 : 21700469 유진수

본 md 파일은, 딥러닝 모델(QR 코드 리더기)을 활용한 제품의 분류 자동화 공정 구현에 대해 다루고 있습니다.

데모 구현을 위한 사전 환경 설정은, 아래의 링크를 참조하십시오.

- UR5e 초기 설정 : 
- QR 코드 리더기 패키지 다운로드 : 
- 컨베이어 벨트 환경 구축 :

<br>

## 공정 개요

물류 산업에서는, QR코드 또는 바코드를 활용하여 물품의 종류를 판별합니다.
또한, 컨베이어 벨트를 활용하여 물품을 이송합니다.

본 프로젝트는 이러한 환경 및 설비로부터 취득한 데이터를 기반으로, 로봇 팔을 제어하는 것을 목적으로 합니다.

본 공정의 개요를 대략적으로 표현하면 아래와 같습니다.

<br>

![image](https://user-images.githubusercontent.com/84503980/206390286-cf8e0846-62fd-44e2-9d32-0f4f629fd023.png)

<br>

**1. 분류 공정 <br>**
컨베이어 벨트를 타고 물품이 운송됩니다. <br>
비전 센서에 4개의 QR 코드가 인식되면 물품이 정상적인 위치에 도달했다고 판단하고, QR 코드의 정보를 로봇에 송신합니다. <br>
이후 수신된 정보를 기반으로, 컨베이어 벨트 좌/우에 놓인 상자에 물품을 분류 적재합니다.

본 프로젝트에서는, A1 & A2 & B1 & B2 라는 정보를 갖는 QR 코드를 생성하였고,
A 상자와 B 상자 안에 물건을 분류 적재하는 방향으로 공정을 설계했습니다.
1과 2를 굳이 나눈 것은, 경우의 수를 늘림으로써 보다 복잡한 공정을 구현하기 위함이었습니다.

**2. 적재 공정 <br>**
시각적인 데모를 위해, 로봇 2개가 상호작용하며 무한히 동작하는 데모를 구축하고자 했습니다.
이에, 분류 이후 다시 물건을 적재함으로써 로봇에 정보를 보내는 공정을 설계했습니다.

분류 공정 수행 당시 어떠한 위치에 물품을 적재했는지 기억합니다.
분류 이후, 난수를 생성하여 임의로 새로운 적재 순서를 정의합니다.
이후, 순서에 맞게 컨베이어 벨트 위의 상자에 물건을 적재합니다.

적재가 끝난 이후에는, 컨베이어 벨트를 동작시켜 제2의 로봇 앞으로 물건을 송신합니다.


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
# 웹캠 전원 On
rosrun usb_cam usb_cam_node

# 이미지 내부 QR 코드 인식, 메세지 송신
rosrun ur_interface Image_Processing.py
```

<br>

### 3. 로봇 제어
```
rosrun ur_interface closed_loop_system
```
