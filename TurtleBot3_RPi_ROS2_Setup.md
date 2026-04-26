# 🐢 TurtleBot3 ROS2 (Humble) on Raspberry Pi (64-bit)

라즈베리파이에서 **ROS2 Humble 기반 TurtleBot3 개발 환경**을 구축하는
전체 가이드입니다.\
Docker + Wayland + GPU 가속 + 센서(LiDAR/Camera/OpenCR)까지 포함된
**실전 구성**입니다.

------------------------------------------------------------------------

## 📦 0. Raspberry Pi OS (64-bit) 설치

-   Raspberry Pi OS 64-bit 설치
-   SSH 활성화

------------------------------------------------------------------------

## 🔌 1. 라즈베리파이 접속

``` bash
ssh pi@SMU
```

문제 시:

``` bash
ssh-keygen -R SMU
ssh pi@SMU
```

------------------------------------------------------------------------

## 🧠 2. Swap 메모리 설정

``` bash
sudo apt update
sudo apt install dphys-swapfile -y
sudo nano /etc/dphys-swapfile
```

    CONFIG_SWAPSIZE=10240

``` bash
sudo reboot
```

------------------------------------------------------------------------

## 🐳 3. Docker 설치

``` bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ${USER}
sudo chmod 666 /var/run/docker.sock
docker version
sudo systemctl enable docker
```

------------------------------------------------------------------------

## 🖥️ 4. VNC + Wayland

``` bash
sudo raspi-config
```

→ Interface Options → VNC Enable

.bashrc:

``` bash
export DISPLAY=:0
xhost +local:docker
```

------------------------------------------------------------------------

## 🚀 5. ROS2 Docker 실행

``` bash
docker run -it --name ros_humble_rpi --net=host --privileged -v /dev:/dev -v /dev/dri:/dev/dri -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY arm64v8/ros:humble
```

------------------------------------------------------------------------

## 📦 6. ROS2 패키지

``` bash
apt update
apt install ros-humble-rviz2 -y
apt install ros-humble-nav2-bringup -y
```

------------------------------------------------------------------------

## 🔨 7. TurtleBot3 빌드

``` bash
mkdir -p ~/turtlebot3_ws/src
cd ~/turtlebot3_ws/src
git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3.git

cd ~/turtlebot3_ws
colcon build --symlink-install --parallel-workers 1
```

------------------------------------------------------------------------

## 🔌 8. 장치 확인

``` bash
ls /dev/ttyUSB0
ls /dev/video0
ls /dev/ttyACM0
```

------------------------------------------------------------------------

## 📷 9. 카메라

``` bash
apt install ros-humble-v4l2-camera -y
ros2 run v4l2_camera v4l2_camera_node
```

------------------------------------------------------------------------

## ⚙️ 10. OpenCR

``` bash
wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
tar -xvf opencr_update.tar.bz2
cd opencr_update
./update.sh /dev/ttyACM0 burger.opencr
```

------------------------------------------------------------------------

## 🎮 11. 실행

``` bash
ros2 launch turtlebot3_bringup robot.launch.py
ros2 run turtlebot3_teleop teleop_keyboard
```

------------------------------------------------------------------------

## ⚡ Tips

-   메모리 부족 → swap 필수
-   rviz 느림 → GPU 설정 확인
-   센서 안됨 → /dev 확인
