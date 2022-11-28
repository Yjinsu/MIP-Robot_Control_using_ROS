# How to Use UR5e?


## 초기 설정

### Go home directory
cd ~ 

### Clone the driver
git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver

### Clone the description. Currently, it is necessary to use the melodic-devel branch.
git clone -b melodic-devel https://github.com/ros-industrial/universal_robot.git src/universal_robot

### Install dependencies
sudo apt update -qq
rosdep update
rosdep install --from-paths src --ignore-src -y

### Build the workspace
catkin_make

### 경로 설정

터미널 실행 시 해당 경로 접근해서 쉘 \
source devel/setup.bash 

현재 경로 확인이 필요하다면? \
cat ~/.bashrc

경로 수정이 필요하다면? \
sudo gedit ~/.bashrc 

조인트만 옮길 수 있는 컨트롤러 다운로드 \
sudo apt install ros-melodic-rqt-joint-trajectory-controller 

sudo apt-get upgrade

