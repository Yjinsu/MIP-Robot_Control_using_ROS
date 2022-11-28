# How to Use UR5e?


## 초기 설정

### Go home directory
cd ~ 

### clone the driver
git clone https://github.com/UniversalRobots/Universal_Robots_ROS_Driver.git src/Universal_Robots_ROS_Driver

### clone the description. Currently, it is necessary to use the melodic-devel branch.
git clone -b melodic-devel https://github.com/ros-industrial/universal_robot.git src/universal_robot

### install dependencies
sudo apt update -qq
rosdep update
rosdep install --from-paths src --ignore-src -y

### build the workspace
catkin_make

### 경로 설정
source devel/setup.bash ///// 터미널 실행 시 해당 경로 접근해서 쉘을 킨다는 의미. 경로 설정해두면 편하다.
cat ~/.bashrc ///// 현재 경로 확인하는 코드
( sudo gedit ~/.bashrc ///// 경로 수정 시 이 코드 입력해서, 파일 수정해주면 된다. )

sudo apt install ros-melodic-rqt-joint-trajectory-controller // 조인트만 옮길 수 있는 컨트롤러 다운로드

sudo apt-get upgrade

