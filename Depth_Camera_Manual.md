# How to Use Realsense Depth camera?

작성자 : 21700469 유진수

참조 : https://github.com/IntelRealSense/realsense-ros

Pyrealsens2 설치법 = https://jstar0525.tistory.com/97
pip가 설치 안 되어있다면? https://jjeongil.tistory.com/1274 참고하여 진행할 것.


<br>

## 1. 환경 설정

<br> 

### ROS Package 설치
```
sudo apt-get install ros-$ROS_DISTRO-realsense2-camera

sudo apt-get install ros-melodic-realsense2*

sudo apt install --reinstall ros-melodic-realsense2-description

```

### Realsense Depth Camera 실행
```
roslaunch realsense2_camera rs_camera.launch
```
launch 파일은 opt/ros/melodic/share/realsense_camera_launch 에 저장되어 있다.


### 연결된 카메라 확인
```
# 이미지 확인이 필요할 때?
rqt

# 연결된 카메라의 포트가 궁금할 때?
ls -ltr /dev/video*
```

## 2. Camera Calibration

1. 코드 실행
```
rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.108 image:=/camera/color/image_raw
```

위 코드 상에서 인가하는 파라미터는 다음과 같다.
- **--size**     -> 체커보드 코너의 개수. 위 코드는, 체커보드 내부에 가로 코너 8개, 세로 코너 6개가 있음을 의미
- **--square**   -> 체커보드 내부 정사각형의 실측 길이 (meter). 위 코드상으론 10.8cm
- **--image:=**  -> 카메라 토픽. rqt를 통해 사용자의 환경을 확인하고 필요시 변경하면 된다.

<br>

2. 코드가 실행된 후? 
- X, Y, Size, Skew 바가 초록색으로 채워질 때까지 체스 보드를 움직인다.

<br>

3. 계산 결과 저장 및 적용 \
Calibration이 완료되면 SAVE 버튼을 눌러서 Calibration 정보 파일을 저장한 뒤 압축을 해제한다.
(Calibration 결과는 tmp 폴더 (opt 폴더와 동일한 위치-ros의 상위 폴더) 에 저장되어 있다)
```
cd /tmp
tar -xvzf calibrationdata.tar.gz
mv ost.txt ost.ini
```


```

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


