# 🤖 Raspberry Pi 4 — Ubuntu 22.04 + XFCE4 + ROS2 Humble 완전 구축 가이드

Windows PC의 MobaXterm(RDP)으로 라즈베리파이 4 원격 데스크탑에 접속하고,  
**Ubuntu 22.04 LTS Server** 위에 Docker 없이 **ROS2 Humble을 네이티브로 설치**하여  
TurtleBot3(Burger)를 구동하는 전체 가이드입니다.

---

## 📋 전체 흐름

```
Ubuntu 22.04 Server 이미지 굽기
        ↓
초기 부팅 & SSH 접속
        ↓
시스템 업데이트 & 한국어 설정
        ↓
XFCE4 데스크탑 설치
        ↓
XRDP 설치 & MobaXterm RDP 접속
        ↓
ROS2 Humble 네이티브 설치
        ↓
TurtleBot3 패키지 빌드
        ↓
✅ ROS2 + GUI 데스크탑 완성
```

---

## 🛠️ 개발 환경

| 항목 | 내용 |
|------|------|
| 하드웨어 | Raspberry Pi 4 (4GB 권장) |
| OS | Ubuntu 22.04 LTS Server (64-bit) |
| 데스크탑 환경 | XFCE4 |
| 원격 접속 서버 | XRDP (Port 3389) |
| 클라이언트 도구 | MobaXterm (Windows) |
| ROS 버전 | ROS2 Humble Hawksbill |
| 로봇 모델 | TurtleBot3 Burger |
| 라이다 모델 | LDS-03 |

---

## 목차

1. [Ubuntu 22.04 LTS Server 이미지 설치](#step-1-ubuntu-2204-lts-server-이미지-설치)
2. [부팅 & SSH 접속](#step-2-부팅--ssh-접속)
3. [시스템 초기 설정](#step-3-시스템-초기-설정)
4. [XFCE4 데스크탑 설치](#step-4-xfce4-데스크탑-설치)
5. [XRDP 설치 및 설정](#step-5-xrdp-설치-및-설정)
6. [Polkit 색상 인증 경고 제거](#step-6-polkit-색상-인증-경고-제거-권장)
7. [MobaXterm RDP 접속](#step-7-mobaxterm-rdp-접속)
8. [스왑 공간 확보](#step-8-스왑-공간-확보)
9. [ROS2 Humble 네이티브 설치](#step-9-ros2-humble-네이티브-설치)
10. [TurtleBot3 패키지 설치 및 빌드](#step-10-turtlebot3-패키지-설치-및-빌드)
11. [OpenCR USB 포트 설정](#step-11-opencr-usb-포트-설정)
12. [도메인 ID 및 라이다 모델 설정](#step-12-도메인-id-및-라이다-모델-설정)
13. [카메라 설정](#step-13-카메라-설정)
14. [OpenCR 펌웨어 설정](#step-14-opencr-펌웨어-설정)
15. [Arduino IDE 설치](#step-15-arduino-ide-설치)
16. [로봇 구동](#step-16-로봇-구동)
17. [트러블슈팅](#-트러블슈팅)

---

## STEP 1. Ubuntu 22.04 LTS Server 이미지 설치

### 필요 도구

- [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
- MicroSD 카드 (32GB 이상 권장)

### OS 선택

```
Other general-purpose OS → Ubuntu → Ubuntu Server 22.04 LTS (64-bit)
```

### ⚙️ 고급 설정 (톱니바퀴 아이콘)

이미지를 굽기 전에 반드시 설정합니다:

| 항목 | 설정값 |
|------|--------|
| Set hostname | `rpi4` |
| Enable SSH | Use password authentication |
| Set username/password | [계정명] / [비밀번호] |
| Configure wireless LAN | Wi-Fi 사용 시 SSID/PW 입력 |
| Set locale | Asia/Seoul / ko_KR |

> 💡 이 설정을 완료하면 첫 부팅부터 바로 SSH 접속이 가능합니다.

---

## STEP 2. 부팅 & SSH 접속

### IP 주소 확인

공유기 관리 페이지에서 확인하거나, 모니터를 직접 연결 후 아래 명령을 실행합니다:

```bash
hostname -I
# 또는
ip addr show | grep "inet "
```

### MobaXterm SSH 접속

```
Session → SSH
  Remote host : 192.168.x.x   ← 라즈베리파이 IP
  Username    : [계정명]
  Port        : 22
```

접속 후 비밀번호 입력 → 터미널 진입 완료

---

## STEP 3. 시스템 초기 설정

```bash
# 시스템 업데이트
sudo apt update && sudo apt full-upgrade -y

# 한국어 로케일 설정 (선택)
sudo locale-gen ko_KR.UTF-8
sudo update-locale LANG=ko_KR.UTF-8

# 타임존 설정
sudo timedatectl set-timezone Asia/Seoul
timedatectl status        # 확인

# 재부팅
sudo reboot
```

> 재부팅 후 다시 SSH로 접속합니다.

---

## STEP 4. XFCE4 데스크탑 설치

```bash
# XFCE4 설치 (경량 데스크탑 환경)
sudo apt install -y xfce4 xfce4-goodies
```

> 설치 중 display manager 선택 팝업이 나타나면 **lightdm** 을 선택합니다.  
> `xfce4-goodies` : 파일 매니저, 텍스트 에디터 등 유틸리티 포함

---

## STEP 5. XRDP 설치 및 설정

```bash
# XRDP 설치
sudo apt install -y xrdp

# xrdp 계정을 ssl-cert 그룹에 추가 (보안 오류 방지)
sudo adduser xrdp ssl-cert

# XFCE4를 기본 세션으로 지정 ← 핵심 설정
echo "xfce4-session" > ~/.xsession
chmod +x ~/.xsession

# XRDP 서비스 자동시작 등록 및 시작
sudo systemctl enable xrdp
sudo systemctl start xrdp

# 상태 확인
sudo systemctl status xrdp
```

정상 실행 시 출력:

```
● xrdp.service - xrdp daemon
   Active: active (running)
```

```bash
# 방화벽 설정 (ufw 활성화된 경우)
sudo ufw allow 3389/tcp
sudo ufw status
```

---

## STEP 6. Polkit 색상 인증 경고 제거 (권장)

접속 시 색상 관리 인증 팝업 오류가 반복되는 현상을 방지합니다.

```bash
sudo nano /etc/polkit-1/localauthority/50-local.d/xrdp-color.pkla
```

아래 내용을 붙여넣습니다:

```ini
[Allow Colord for XRDP]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
```

저장 후 XRDP를 재시작합니다:

```bash
# Ctrl+O → Enter → Ctrl+X 로 저장
sudo systemctl restart xrdp
```

---

## STEP 7. MobaXterm RDP 접속

### 접속 설정

```
MobaXterm 실행
  → Session 클릭
  → RDP 탭 선택
  → Remote host : 192.168.x.x   ← 라즈베리파이 IP
  → Username    : [계정명]
  → Port        : 3389
  → OK → 비밀번호 입력
```

### 접속 성공 시 화면 순서

```
XRDP 로그인 화면 (파란 로고)
        ↓
username / password 입력
        ↓
XFCE4 데스크탑 로딩
        ↓
✅ GUI 데스크탑 완성
```

> 첫 접속 시 Update Notifier 팝업이 표시됩니다. 터미널에서 직접 처리합니다:
> ```bash
> sudo apt update && sudo apt full-upgrade -y
> sudo reboot
> ```

---

## STEP 8. 스왑 공간 확보

ROS2 빌드 중 메모리 부족(OOM)으로 멈추는 현상을 방지하기 위해 Swap을 확장합니다.

```bash
free -h
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

## STEP 9. ROS2 Humble 네이티브 설치

> Ubuntu 22.04 LTS에서 ROS2 Humble을 직접 설치합니다. (Docker 불필요)

### 1단계: 로케일 설정

```bash
sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # 확인
```

### 2단계: ROS2 저장소 추가

```bash
sudo apt install software-properties-common -y
sudo add-apt-repository universe

sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
  -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
  http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" \
  | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

### 3단계: ROS2 Humble 설치

```bash
sudo apt update
sudo apt upgrade -y

# ROS2 Desktop 설치 (rviz2 포함)
sudo apt install ros-humble-desktop -y

# 개발 도구 설치
sudo apt install ros-dev-tools -y
```

> ⚠️ 라즈베리파이 4에서 `ros-humble-desktop` 설치는 15~30분 소요될 수 있습니다.  
> 저장 공간 절약이 필요한 경우 `ros-humble-ros-base` 로 대체 가능합니다.

### 4단계: 환경 설정

```bash
echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc
source ~/.bashrc

# 설치 확인
ros2 --version
```

---

## STEP 10. TurtleBot3 패키지 설치 및 빌드

> 예상 소요 시간: 약 15~25분

### 의존성 설치

```bash
sudo apt install -y \
  python3-argcomplete \
  python3-colcon-common-extensions \
  libboost-system-dev \
  build-essential

sudo apt install -y \
  ros-humble-hls-lfcd-lds-driver \
  ros-humble-turtlebot3-msgs \
  ros-humble-dynamixel-sdk \
  ros-humble-nav2-bringup \
  ros-humble-xacro \
  ros-humble-rviz2 \
  ros-humble-joint-state-publisher-gui \
  ros-humble-tf-transformations \
  libudev-dev
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

```bash
cd ~/turtlebot3_ws/
rosdep update
rosdep install --from-paths src --ignore-src -r -y
colcon build --symlink-install --parallel-workers 1
```

> ⚠️ `--parallel-workers 1` 옵션은 라즈베리파이 4의 메모리 부족(OOM)으로 인한 빌드 실패를 방지합니다.

```bash
echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
source ~/.bashrc
```

---

## STEP 11. OpenCR USB 포트 설정

```bash
cp `ros2 pkg prefix turtlebot3_bringup`/share/turtlebot3_bringup/script/99-turtlebot3-cdc.rules \
  /etc/udev/rules.d/

sudo udevadm control --reload-rules
sudo udevadm trigger
```

### 장치 인식 확인

```bash
ls /dev/tb3-lidar   # 라이다 (LDS-03)
ls /dev/ttyUSB0     # USB 카메라
ls /dev/ttyACM0     # OpenCR (아두이노)
```

---

## STEP 12. 도메인 ID 및 라이다 모델 설정

`~/.bashrc`에 추가합니다:

```bash
echo 'export ROS_DOMAIN_ID=20 #TURTLEBOT3' >> ~/.bashrc
echo 'export LDS_MODEL=LDS-03' >> ~/.bashrc
echo 'export TURTLEBOT3_MODEL=burger' >> ~/.bashrc
source ~/.bashrc
```

---

## STEP 13. 카메라 설정

### 1단계: 장치 인식 확인

```bash
ls -l /dev/video*
# 일반적으로 /dev/video0 이 기본 카메라
```

### 2단계: v4l2 카메라 패키지 설치 및 실행

```bash
sudo apt install -y ros-humble-v4l2-camera ros-humble-image-transport-plugins v4l-utils

v4l2-ctl --list-devices

# 카메라 노드 실행
ros2 run v4l2_camera v4l2_camera_node
```

### 3단계: rviz2에서 영상 확인

```bash
rviz2
```

rviz2 내에서 `Add → By topic → /image_raw` 를 선택합니다.

### 4단계: Foxglove에서 영상 확인 (선택)

```bash
sudo apt install -y ros-humble-foxglove-bridge

ros2 run foxglove_bridge foxglove_bridge \
  --ros-args \
  -p send_buffer_limit:=10000000 \
  -p use_compression:=true
```

---

## STEP 14. OpenCR 펌웨어 설정

### 1단계: 환경 변수 설정

```bash
export OPENCR_PORT=/dev/ttyACM0
export OPENCR_MODEL=burger
rm -rf ./opencr_update.tar.bz2
```

### 2단계: 펌웨어 다운로드

```bash
cd ~
sudo apt install -y wget tar
wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS2/latest/opencr_update.tar.bz2
tar -xvf opencr_update.tar.bz2
```

### 3단계: 펌웨어 업로드

```bash
cd ./opencr_update
./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr
```

> 아두이노 IDE에서도 확인 가능합니다:  
> `파일 → 예제 → Turtlebot3 ROS2 → turtlebot3_burger`

### 4단계: OpenCR 동작 테스트

배터리 전원 연결 후 모터 전원 스위치를 켠 다음, 로봇을 **1미터 이상 넓은 공간**에 놓습니다.

| 버튼 | 동작 |
|------|------|
| `PUSH SW 1` 길게 누르기 | 30cm 전진 |
| `PUSH SW 2` 길게 누르기 | 제자리 180도 회전 |

> 동작이 안 될 경우, 아두이노 IDE에서 다음 예제를 실행합니다:  
> `파일 → 예제 → Turtlebot3 → turtlebot3_setup → turtlebot3_setup_motor`

---

## STEP 15. Arduino IDE 설치

1. [ROBOTIS 공식 가이드](https://emanual.robotis.com/docs/en/software/arduino_ide/)에서 Arduino IDE 설치
   - Windows 11에서는 STM32 드라이버 별도 설치 불필요

2. `File → Preferences → Additional boards manager URLs` 에 다음 URL 추가:
   ```
   https://raw.githubusercontent.com/ROBOTIS-GIT/OpenCR/master/arduino/opencr_release/package_opencr_index.json
   ```

3. 보드 매니저에서 **OpenCR 1.5.2** 설치
   > ⚠️ 1.5.3은 bzip 오류 발생 / Arduino IDE 2.3.8에서는 정상 설치 가능

4. 라이브러리 매니저에서 **Dynamixel2Arduino** 설치

---

## STEP 16. 로봇 구동

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

### rqt 설치 및 실행

```bash
sudo apt install -y ros-humble-rqt*
rqt
```

---

## 📝 최종 구성 요약

```
┌─────────────────────────────────────┐
│      Windows PC (MobaXterm)         │
│      RDP Client  →  Port 3389       │
└──────────────┬──────────────────────┘
               │ RDP Protocol
               ▼
┌─────────────────────────────────────┐
│       Raspberry Pi 4                │
│       Ubuntu 22.04 LTS Server       │
│       ├── XRDP  (Port 3389)         │
│       ├── XFCE4 Desktop             │
│       ├── ROS2 Humble (Native)      │
│       └── TurtleBot3 Workspace      │
└─────────────────────────────────────┘
```

### `~/.bashrc` 최종 설정 정리

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
| USB 카메라 | `/dev/video0` |
| OpenCR (아두이노) | `/dev/ttyACM0` |

---

## 🔧 트러블슈팅

| 증상 | 원인 | 해결 방법 |
|------|------|-----------|
| 접속 후 회색 빈 화면 | `~/.xsession` 파일 없음 | `echo "xfce4-session" > ~/.xsession` 실행 |
| 포트 연결 거부 | xrdp 서비스 미실행 | `sudo systemctl start xrdp` |
| 로그인 후 바로 끊김 | 기존 SSH 세션 충돌 | SSH에서 먼저 로그아웃 후 RDP 접속 |
| 화면 깨짐 / 해상도 이상 | 해상도 불일치 | MobaXterm RDP 설정에서 해상도 수동 조정 |
| 색상 인증 팝업 반복 | polkit 설정 없음 | STEP 6 의 pkla 파일 생성 |
| colcon build 중 멈춤 | 메모리 부족(OOM) | Swap 10GB 확보 후 `--parallel-workers 1` 옵션으로 재빌드 |
| `/dev/tb3-lidar` 없음 | udev rules 미적용 | `sudo udevadm control --reload-rules && sudo udevadm trigger` |
| `ros2` 명령어 없음 | bashrc 미적용 | `source ~/.bashrc` 또는 터미널 재시작 |

---

## 🔗 관련 링크

- [ROBOTIS TurtleBot3 공식 문서](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [ROS2 Humble 설치 가이드](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)
- [OpenCR GitHub](https://github.com/ROBOTIS-GIT/OpenCR)
- [TurtleBot3 GitHub](https://github.com/ROBOTIS-GIT/turtlebot3)
- [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
- [MobaXterm](https://mobaxterm.mobatek.net/)
