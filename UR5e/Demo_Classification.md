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

![image](https://user-images.githubusercontent.com/84503980/206390286-cf8e0846-62fd-44e2-9d32-0f4f629fd023.png)



<br>

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
