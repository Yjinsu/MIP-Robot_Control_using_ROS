# 이슈사항 발생 시 해결 방법

참조 : https://github.com/hyKangHGU/ROS_Ubuntu_18_04/blob/main/ROS%20-%20Python3_version_up.md

<br>

### 패키지를 다운 받았는데, 계속 없다는 에러가 발생할 경우?
- 경로 문제일 가능성이 농후하다. 아래의 코드를 통해 경로를 확인하고, 필요시 수정하라
```
# 현재 경로 확인
cat ~/.bashrc

# 경로 설정이 안 된 경우
source devel/setup.bash #터미널 실행 시 해당 경로 접근해서 쉘을 킨다는 의미. 경로 설정해두면 편하다.

# 경로가 본인의 작업 공간과 다른 경우
sudo gedit ~/.bashrc
```

<br>

### em 모듈이 없다는 오류가 발생할 경우?

- 모듈을 다운 받아 주면, 가볍게 해결된다.

```
sudo apt install python3-empy
```

<br>

### 스크립트 파일이 실행되지 않는 경우?

- 작업 공간(스크립트 파일이 위치한 경로)에 들어간 뒤, 파일 확장자를 확인하기

```
ls -al
```

- 파이썬 코드의 경우, +x 파일이 아니면 실행되지 않는다. 확장자는 아래의 코드로 바꿀 수 있다.
```
chmod +x filename.py
```
