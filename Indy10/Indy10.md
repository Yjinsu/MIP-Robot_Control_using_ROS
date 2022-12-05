# How to Use Indy10?

작성자 : 21700469 유진수


<br>

## 1. 환경 설정

<br>

### 작업 공간 생성 & Git Clone

아래 코드를 copy & paste 할 것.

```
# Go home directory
cd ~ 


# 작업 공간 생성
mkdir -p indy10_ws/src


# Download the package




# Install dependencies
sudo apt update -qq
rosdep update
rosdep install --from-paths src --ignore-src -y


# Build the workspace
catkin_make
```

### 경로 설정
```
# 터미널 실행 시 해당 경로에 접근, 쉘 활성화 (환경설정 초기 1회만 수행)
source devel/setup.bash 

# 현재 경로 확인이 필요하다면?
cat ~/.bashrc

#경로 수정이 필요하다면?
sudo gedit ~/.bashrc 
```


<br>

## 2. 로봇-컴퓨터 간 IP 연결

<br>


```
# 로봇 연결 + 시뮬레이션 실행
roslaunch indy10_moveit_config moveit_planning_execution.launch robot_ip:=192.168.0.6

# 오직 시뮬레이션만 실행
roslaunch indy10_gazebo indy10_moveit_gazebo.launch
```

## 3. 카메라 전원 On & 이미지 프로세싱
```
# with align -> 얘 실행시킬 것!
roslaunch realsense2_camera rs_camera.launch align_depth:=true

# without align
roslaunch realsense2_camera rs_camera.launch

# 카메라 포트 확인 코드 (Depth Camera가 잘 연결되었는지 확인
ls -ltr /dev/video*

# 카메라 이미지 수신&영상처리 기법 적용, 메세지 송신
rosrun indy_driver Image_Processing.py

```

<br>

## 4. 로봇 실제 구동

<br>

```
rosrun indy_driver Robot_Controller.py
```
