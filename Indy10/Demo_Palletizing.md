# Demo: Palletizing

작성자 : 21700469 유진수

본 md 파일은 팔레타이징, 즉 물류 적재 공정 구현에 대해 다루고 있습니다.

데모 구현을 위한 사전 환경 설정은, 아래의 링크를 참조하십시오.

- Indy10 초기 설정 : 
- Depth Camera Setting : 


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
roslaunch indy10_gazebo indy10_moveit_gazebo.launch

# Real
roslaunch indy10_moveit_config moveit_planning_execution.launch robot_ip:=192.168.0.6
```

<br>

### 2. 카메라 전원 On & 이미지 프로세싱

```
# Color Frame과 Depth Frame 동기화(with align) -> 얘 실행시킬 것!
roslaunch realsense2_camera rs_camera.launch align_depth:=true

# without align (참고 목적으로 기록하였으나, 실행시키지 않습니다)
roslaunch realsense2_camera rs_camera.launch

# 카메라 포트 확인 코드 (Depth Camera가 잘 연결되었는지 확인하고 싶은 경우에만 실행합니다)
ls -ltr /dev/video*

# 카메라 이미지 수신&영상처리 기법 적용, 메세지 송신
rosrun indy_driver Image_Processing.py
```

<br>

### 3. 로봇 제어 코드 실행
```
rosrun indy_driver Robot_Controller.py
```

