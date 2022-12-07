# Demo: Palletizing

작성자 : 21700469 유진수

본 md 파일은 팔레타이징, 즉 물류 적재 공정 구현에 대해 다루고 있습니다.

데모 구현을 위한 사전 환경 설정은, 아래의 링크를 참조하십시오.

- Indy10 초기 설정 : 


<br>

## 공정 개요

본 공정은, ~ 입니다.

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
