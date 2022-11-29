# MIP_Demo

작성자 : 21700469 유진수


<br>

## 1. 로봇-노트북 연결
```
# Simulation
roslaunch ur_gazebo ur5e_bringup.launch
roslaunch ur5e_sim_moveit_config move_group.launch

# Real
roslaunch ur_robot_driver ur5e_bringup.launch robot_ip:=192.168.0.2
roslaunch ur5e_real_moveit_config move_group.launch
```

<br>

## 2. 이미지 취득
```
# 웹캠 전원 On
rosrun usb_cam usb_cam_node

# 이미지 내부 QR 코드 인식, 메세지 송신
rosrun ur_interface Image_Processing.py
```

<br>

## 3. 로봇 제어
```

```
