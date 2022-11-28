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
mkdir -p handong_ws/src


# Clone the driver
git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver


# Clone the description. Currently, it is necessary to use the melodic-devel branch.
git clone -b melodic-devel https://github.com/ros-industrial/universal_robot.git src/universal_robot


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

### 조인트를 조절할 수 있는 컨트롤러 다운로드
```
sudo apt install ros-melodic-rqt-joint-trajectory-controller 

sudo apt-get upgrade
```

<br>

## 2. 시뮬레이션

<br>

### UR Gazebo 실행
```
roslaunch ur_gazebo ur5e_bringup.launch

roslaunch ur5e_sim_moveit_config move_group.launch

# 조인트 컨트롤러가 잘 동작되는지 시뮬레이션으로 확인하고 싶다면?
rosrun rqt_joint_trajectory_controller rqt_joint_trajectory_controller 
```




### 웹캠 카메라 전원 On & 이미지 프로세싱
```
rosrun usb_cam usb_cam_node

rosrun ur_interface Image_Processing.py
```

<br>

## 3. 로봇 실제 구동

<br>

### UR5e와 컴퓨터 간 IP 연결
```
roslaunch ur_robot_driver ur5e_bringup.launch robot_ip:=192.168.0.2

roslaunch ur5e_real_moveit_config move_group.launch
```

### 웹캠 카메라 전원 On & 이미지 프로세싱
```
rosrun usb_cam usb_cam_node

rosrun ur_interface Image_Processing.py
```


