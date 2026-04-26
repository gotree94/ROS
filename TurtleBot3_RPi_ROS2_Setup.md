# 🤖 TurtleBot3 ROS2 Humble - 라즈베리파이 설치 가이드

라즈베리파이 4에서 Docker 기반으로 ROS2 Humble 환경을 구축하고, TurtleBot3(Burger)를 구동하기 위한 전체 설치 가이드입니다.

---

## 📋 목차

1. [라즈베리파이 64비트 OS 설치](#1-라즈베리파이-64비트-os-설치)
2. [SSH 접속](#2-ssh-접속)
3. [스왑 공간 확보](#3-스왑-공간-확보)
4. [Docker 설치](#4-docker-설치)
5. [WayVNC 서버 활성화](#5-wayvnc-서버-활성화)
6. [ROS2 Humble 컨테이너 설치](#6-ros2-humble-컨테이너-설치)
7. [ROS2 패키지 설치 1](#7-ros2-패키지-설치-1)
8. [ROS2 패키지 설치 및 빌드 2](#8-ros2-패키지-설치-및-빌드-2)
9. [OpenCR USB 포트 설정](#9-opencr-usb-포트-설정)
10. [도메인 ID 및 라이다 모델 설정](#10-도메인-id-및-라이다-모델-설정)
11. [카메라 설정](#11-카메라-설정)
12. [OpenCR 펌웨어 설정](#12-opencr-펌웨어-설정)
13. [Arduino IDE 설치](#13-arduino-ide-설치)
14. [로봇 구동](#14-로봇-구동)

---

## 1. 라즈베리파이 64비트 OS 설치

Raspberry Pi Imager를 사용하여 **Raspberry Pi OS (64-bit)** 를 설치합니다.

> ⚠️ 반드시 **64비트** 버전을 설치해야 합니다. ROS2 Humble arm64 Docker 이미지와의 호환성이 요구됩니다.

---

## 2. SSH 접속

Windows PowerShell에서 라즈베리파이에 SSH로 접속합니다.

```bash
ssh pi@SMU
```

SSH 키 충돌 오류가 발생할 경우, 기존 키를 삭제 후 재접속합니다:

```bash
ssh-keygen -R SMU
ssh pi@SMU
```

---

## 3. 스왑 공간 확보

빌드 중 메모리 부족으로 멈추는 현상을 방지하기 위해 Swap을 **2GB~10GB**로 확장합니다.

```bash
free -h
sudo apt update
sudo apt install dphys-swapfile -y
sudo nano /etc/dphys-swapfile
```

파일 내에서 다음 값을 설정합니다:

```
CONFIG_SWAPSIZE=10240
```

저장 후 재부팅합니다:

```bash
sudo reboot
```

---

## 4. Docker 설치

> 예상 소요 시간: 약 3분

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ${USER}
groups ${USER}
sudo chmod 666 /var/run/docker.sock
docker version                    # 설치 확인
sudo systemctl enable docker      # 부팅 시 자동 실행
```

---

## 5. WayVNC 서버 활성화

### raspi-config에서 VNC 활성화

```
sudo raspi-config > 3 Interface Options > I3 VNC > Yes > OK > Finish
```

### TigerVNC 클라이언트 설치 (Windows)

아래 링크에서 TigerVNC를 다운로드하여 기본 설치합니다:

🔗 https://sourceforge.net/projects/tigervnc/postdownload

### 디스플레이 환경 설정

TigerVNC로 라즈베리파이에 접속한 후, 터미널에서 다음을 실행합니다:

```bash
# Wayland 세션 확인
echo $XDG_SESSION_TYPE   # wayland 가 출력되어야 함

# 디스플레이 설정
echo $DISPLAY             # :0 이 출력되어야 함
xhost +local:docker
```

`~/.bashrc` 에 영구 설정을 추가합니다:

```bash
nano ~/.bashrc
```

다음 내용을 추가합니다:

```bash
export DISPLAY=:0
xhost +local:docker
```

저장 후 적용합니다:

```bash
source ~/.bashrc
```

> 💡 rviz2가 실행되지 않을 경우: `xhost +local:` 을 실행하세요.

---

## 6. ROS2 Humble 컨테이너 설치

> ⚠️ TigerVNC 터미널에서 실행하세요.

```bash
docker run -it \
  --name ros_humble_rpi \
  --net=host \
  --privileged \
  --restart unless-stopped \
  -v /dev:/dev \
  -v /dev/dri:/dev/dri \
  -v /etc/udev/rules.d:/etc/udev/rules.d \
  -v /run/udev:/run/udev:ro \
  -v /dev/shm:/dev/shm \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v /run/user/1000/wayland-0:/run/user/1000/wayland-0 \
  -v $HOME/.Xauthority:/root/.Xauthority:ro \
  -e DISPLAY=$DISPLAY \
  -e WAYLAND_DISPLAY=$WAYLAND_DISPLAY \
  -e XDG_RUNTIME_DIR=/run/user/1000 \
  -e XAUTHORITY=/root/.Xauthority \
  -e QT_X11_NO_MITSHM=1 \
  -e LD_LIBRARY_PATH=/usr/lib/aarch64-linux-gnu/mesa-egl:/usr/lib/aarch64-linux-gnu/mesa-vulkan \
  arm64v8/ros:humble
```

### Docker 실행 옵션 설명

| 옵션 | 역할 |
|------|------|
| `--net=host` | 호스트 네트워크 공유 (ROS2 DDS 통신) |
| `--privileged` | 하드웨어 장치 직접 접근 |
| `--restart unless-stopped` | 재부팅 시 자동 재시작 |
| `-v /dev:/dev` | USB 장치 실시간 인식 |
| `-v /tmp/.X11-unix` | X11 GUI 화면 출력 |
| `-v /run/user/1000/wayland-0` | Wayland GUI 화면 출력 |
| `-e LD_LIBRARY_PATH=...` | Mesa GPU 드라이버 (rviz2 가속) |
| `-v /dev/shm:/dev/shm` | 공유 메모리 (대용량 카메라/포인트 클라우드) |
| `-e QT_X11_NO_MITSHM=1` | Qt 원격 환경 렌더링 오류 방지 |

컨테이너 진입 확인:

```bash
cat /etc/os-release
```

---

## 7. ROS2 패키지 설치 1

> 예상 소요 시간: 약 15분 (컨테이너 내부에서 실행)

```bash
apt update
apt install ros-humble-xacro -y
apt install ros-humble-rviz2 -y
apt install ros-humble-joint-state-publisher-gui -y
apt install ros-humble-tf-transformations -y
apt install ros-humble-nav2-bringup -y
apt install tree -y
apt install imagemagick -y
```

---

## 8. ROS2 패키지 설치 및 빌드 2

> 예상 소요 시간: 약 11분 (컨테이너 내부에서 실행)

### 의존성 설치

```bash
apt install python3-argcomplete python3-colcon-common-extensions libboost-system-dev build-essential -y
apt install ros-humble-hls-lfcd-lds-driver -y
apt install ros-humble-turtlebot3-msgs -y
apt install ros-humble-dynamixel-sdk -y
apt install libudev-dev -y
```

### 소스 클론 및 빌드

```bash
mkdir -p ~/turtlebot3_ws/src && cd ~/turtlebot3_ws/src

git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone -b humble https://github.com/ROBOTIS-GIT/ld08_driver.git
git clone -b humble https://github.com/ROBOTIS-GIT/coin_d4_driver

# 불필요한 패키지 제거
cd ~/turtlebot3_ws/src/turtlebot3
rm -r turtlebot3_cartographer turtlebot3_navigation2
```

### 빌드

```bash
cd ~/turtlebot3_ws/
echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc
source ~/.bashrc
rosdep update
rosdep install --from-paths src --ignore-src -r -y
colcon build --symlink-install --parallel-workers 1
echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
source ~/.bashrc
```

> ⚠️ `--parallel-workers 1` 옵션은 라즈베리파이 4의 메모리 부족(OOM)으로 인한 빌드 실패를 방지합니다.

---

## 9. OpenCR USB 포트 설정

### 컨테이너(ros:humble) 내부에서 실행

```bash
cp `ros2 pkg prefix turtlebot3_bringup`/share/turtlebot3_bringup/script/99-turtlebot3-cdc.rules /etc/udev/rules.d/
```

### 호스트(라즈베리파이) 터미널에서 실행

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

### 장치 인식 확인 (컨테이너 내부)

```bash
ls /dev/tb3-lidar   # 라이다
ls /dev/ttyUSB0     # USB 카메라
ls /dev/ttyACM0     # OpenCR (아두이노)
```

---

## 10. 도메인 ID 및 라이다 모델 설정

컨테이너 내부의 `~/.bashrc`에 추가합니다:

```bash
echo 'export ROS_DOMAIN_ID=20 #TURTLEBOT3' >> ~/.bashrc
echo 'export LDS_MODEL=LDS-03' >> ~/.bashrc   # LDS-03 사용 시
source ~/.bashrc
```

---

## 11. 카메라 설정

### 1단계: 장치 인식 확인

```bash
ls -l /dev/video*
# 일반적으로 /dev/video0 이 기본 카메라
```

### 2단계: v4l2 카메라 패키지 설치 및 실행

```bash
apt update
apt-get install ros-humble-v4l2-camera ros-humble-image-transport-plugins v4l-utils -y
v4l2-ctl --list-devices

# 카메라 노드 실행
ros2 run v4l2_camera v4l2_camera_node
```

### 3단계: rviz2에서 영상 확인

```bash
# rviz2 실행
rviz2
```

rviz2 내에서 `Add → By topic → /image_raw` 를 선택합니다.

> rviz2가 실행되지 않을 경우, 호스트 터미널에서 다음을 실행하세요:
> ```bash
> xhost +local:docker
> ```

### 4단계: Foxglove에서 영상 확인 (선택)

```bash
apt install ros-humble-foxglove-bridge -y
ros2 run foxglove_bridge foxglove_bridge \
  --ros-args \
  -p send_buffer_limit:=10000000 \
  -p use_compression:=true
```

---

## 12. OpenCR 펌웨어 설정

> 컨테이너(ros:humble) 내부에서 실행합니다.

### 1단계: armhf 아키텍처 지원 추가

```bash
dpkg --add-architecture armhf
apt-get update
apt-get install libc6:armhf
```

### 2단계: 환경 변수 설정

```bash
export OPENCR_PORT=/dev/ttyACM0
export OPENCR_MODEL=burger
rm -rf ./opencr_update.tar.bz2
```

### 3단계: 펌웨어 다운로드

```bash
cd
apt install wget tar -y
wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
tar -xvf opencr_update.tar.bz2
```

### 4단계: 펌웨어 업로드

```bash
cd ./opencr_update
./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr
```

> 아두이노 IDE에서 해당 예제를 확인할 수 있습니다:
> `파일 → 예제 → Turtlebot3 ROS2 → turtlebot3_burger`

### 5단계: OpenCR 동작 테스트

배터리 전원 연결 후 모터 전원 스위치를 켠 다음, 로봇을 **1미터 이상 넓은 공간**에 놓습니다.

| 버튼 | 동작 |
|------|------|
| `PUSH SW 1` 길게 누르기 | 30cm 전진 |
| `PUSH SW 2` 길게 누르기 | 제자리 180도 회전 |

동작이 안 될 경우, 아두이노 IDE에서 다음 예제를 실행합니다:

```
파일 → 예제 → Turtlebot3 → turtlebot3_setup → turtlebot3_setup_motor
```

---

## 13. Arduino IDE 설치

### 설치 및 보드 설정 (Windows / Linux)

1. [ROBOTIS 공식 가이드](https://emanual.robotis.com/docs/en/software/arduino_ide/)에서 Arduino IDE 설치
   - Windows 11에서는 STM32 드라이버 별도 설치 불필요

2. `File → Preferences → Additional boards manager URLs` 에 다음 URL 추가:
   ```
   https://raw.githubusercontent.com/ROBOTIS-GIT/OpenCR/master/arduino/opencr_release/package_opencr_index.json
   ```

3. 보드 매니저에서 **OpenCR 1.5.2** 설치
   > ⚠️ 1.5.3은 bzip 오류 발생 / Arduino IDE 2.3.8에서는 정상 설치 가능

4. 라이브러리 매니저에서 **Dynamixel2Arduino** 설치

### 참고 링크

- [OpenCR 예제](https://emanual.robotis.com/docs/en/parts/controller/opencr10/)
- [Dynamixel 설정 가이드](https://emanual.robotis.com/docs/en/platform/turtlebot3/faq/#setup-dynamixels-for-turtlebot3)

---

## 14. 로봇 구동

### 환경 변수 설정

`~/.bashrc`에 다음 내용을 추가합니다:

```bash
export TURTLEBOT3_MODEL=burger
```

### 로봇 런치

```bash
# OpenCR 보드 리셋 버튼을 먼저 눌러줍니다
source ~/.bashrc
ros2 launch turtlebot3_bringup robot.launch.py
```

### 키보드로 조종

새 터미널에서 실행합니다:

```bash
source ~/.bashrc
ros2 run turtlebot3_teleop teleop_keyboard
```

### rqt 설치

```bash
apt install ros-humble-rqt* -y
```

---

## 📝 참고 사항

### `.bashrc` 최종 설정 정리

컨테이너 내부의 `~/.bashrc` 최종 상태 예시입니다:

```bash
source /opt/ros/humble/setup.bash
source ~/turtlebot3_ws/install/setup.bash
export ROS_DOMAIN_ID=20
export LDS_MODEL=LDS-03
export TURTLEBOT3_MODEL=burger
```

### 주요 장치 경로 요약

| 장치 | 경로 |
|------|------|
| 라이다 (LDS-03) | `/dev/tb3-lidar` |
| USB 카메라 | `/dev/ttyUSB0` 또는 `/dev/video0` |
| OpenCR (아두이노) | `/dev/ttyACM0` |

---

## 🔗 관련 링크

- [ROBOTIS TurtleBot3 공식 문서](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [ROS2 Humble 공식 문서](https://docs.ros.org/en/humble/)
- [OpenCR GitHub](https://github.com/ROBOTIS-GIT/OpenCR)
- [TurtleBot3 GitHub](https://github.com/ROBOTIS-GIT/turtlebot3)
