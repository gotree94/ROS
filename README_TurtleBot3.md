# TurtleBot3 Burger — 환경설치

https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/

## TurtleBot3 Burger — 라즈베리파이

* 터틀봇3(TurtleBot3)를 라즈베리 파이에 설치할 때 버전 충돌로 고생하셨던 경험은 많은 개발자가 겪는 고질적인 문제입니다.
* 하드웨어(SBC), OS(Ubuntu), 그리고 ROS 버전이 삼박자로 맞아야 하기 때문입니다.
* 2026년 현재 시점에서 가장 안정적이고 권장되는 조합은 ROS 2 Humble을 기반으로 한 환경입니다.

-----

### 1. 가장 안정적인 추천 조합 (골든 셋업)
* 현재 가장 광범위하게 검증되었으며, 커뮤니티 지원과 튜토리얼이 가장 풍부한 조합입니다.

| 구분	| 추천 사양	| 비고 |
| :-----:| :-----:| :-----:| 
| SBC (하드웨어)	| Raspberry Pi 4 (4GB 이상)	| Pi 3B+는 메모리 부족으로 Humble 구동 시 불안정할 수 있음 | 
| OS	| Ubuntu 22.04.x LTS (64-bit)	| Desktop 버전보다 Server 버전 설치 후 필요한 패키지만 구성 권장 | 
| ROS 버전	| ROS 2 Humble Hawksbill	| 2027년까지 지원되는 장기 지원 버전(LTS)으로 가장 안정적 | 
| Middleware	| Fast DDS (Default)	| Cyclone DDS보다 안정성 면에서 현재 더 선호됨 | 

-----

### 2. 왜 Jazzy나 Noetic이 아닌 Humble인가?
   * Noetic (ROS 1):
      * 이미 EOL(지원 종료)되었거나 종료 직전입니다. 
      * 최신 센서 드라이버나 라이브러리 업데이트가 끊겨 장기적으로는 비추천합니다.
   * Jazzy (ROS 2):
      * 가장 최신 버전이지만, 아직 터틀봇3의 하드웨어 드라이버나 turtlebot3_simulations 패키지 등에서 미세한 버그가 보고되기도 합니다. 
      * 특히 튜토리얼의 문법 체계가 Humble과 달라 초보자가 참고 자료를 찾기 어렵습니다.
   * Humble:
      * ROBOTIS 공식 매뉴얼이 가장 완벽하게 대응하며, OpenCR과의 펌웨어 호환성이 가장 높습니다.

-----

### 3. 설치 시 실패 확률을 낮추는 핵심 팁
   * 설치 중 "왜 안 되지?"를 방지하기 위한 체크리스트입니다.

1.	Ubuntu 이미지 선택: 
   * 반드시 64-bit 버전을 사용하세요. ROS 2는 32-bit 환경에서 성능 저하와 패키지 누락이 심합니다.
2.	Remote PC와 버전 일치: 
   * 라즈베리 파이에 Humble을 깔았다면, 조종하는 PC(Remote PC)도 
   * 반드시 Ubuntu 22.04 + ROS 2 Humble이어야 합니다. 버전이 다르면 토픽이 보이지 않거나 노드가 죽는 현상이 빈번합니다.
3.	ROS_DOMAIN_ID 설정: 
   * 같은 네트워크 환경에 여러 대의 로봇이 있다면 .bashrc 파일에서 export ROS_DOMAIN_ID=X (X는 0~232 사이의 숫자)를 동일하게 맞춰야 통신이 됩니다.
4.	LDS-01/02 드라이버: 
   * 본인의 터틀봇에 달린 라이다 센서 모델을 확인하고 그에 맞는 드라이버를 설치해야 합니다.

-----

### 4. 빠른 설치 가이드 (요약)
   * 라즈베리 파이 터미널에서 아래 순서로 접근하는 것이 가장 안전합니다.

1.	Official Image 사용: 
   * 가능하면 ROBOTIS에서 제공하는 TurtleBot3 SBC 전용 이미지를 굽는 것이 가장 빠릅니다. (이미 ROS2 Humble이 사전 설정됨)
2.	수동 설치 시: 
   * Ubuntu 22.04 Server 설치 -> ROS 2 Humble 설치 -> turtlebot3_bringup 빌드 순서로 진행하세요.

참고: 만약 최신 기능을 위해 꼭 Jazzy를 사용해야 한다면, Docker를 이용한 컨테이너 환경에서 구동하는 것을 권장합니다. 
      네이티브 설치는 아직 라이브러리 의존성 문제가 발생할 확률이 높습니다.

-----

* rp4ros-nwk

```
PS C:\Users\Administrator> ping rp4ros-nwk.local -4

Ping rp4ros-nwk.local [192.168.0.28] 32바이트 데이터 사용:
192.168.0.28의 응답: 바이트=32 시간=2ms TTL=64
192.168.0.28의 응답: 바이트=32 시간=2ms TTL=64
192.168.0.28의 응답: 바이트=32 시간=2ms TTL=64
192.168.0.28의 응답: 바이트=32 시간=3ms TTL=64

192.168.0.28에 대한 Ping 통계:
    패킷: 보냄 = 4, 받음 = 4, 손실 = 0 (0% 손실),
왕복 시간(밀리초):
    최소 = 2ms, 최대 = 3ms, 평균 = 2ms
PS C:\Users\Administrator>
```

<img src="rp4-ros-install\rp4-ros-install_003.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_004.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_005.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_006.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_007.png"> <br>

------

🐢 터틀봇3 주요 기능 호환성 테이블 (2026 업데이트)

| 기능 (Features) | Noetic (ROS 1) | Humble (LTS) | Jazzy (Latest) | 비고  | 
|:---------:|:---------:|:---------:|:---------:|:---------:|
| Teleop (원격 조종) | ✓ | ✓ | ✓ | 기본 패키지 포함 |
| SLAM (지도 작성) | ✓ | ✓ | ✓ | Toolbox/Cartographer 지원 |
| Navigation (주행) | ✓ (Nav1) | ✓ (Nav2) | ✓ (Nav2) | Jazzy는 최신 Nav2 최적화 포함 |
| Simulation (Gazebo) | ✓ (Classic) | ✓ (Classic/Sim) | ✓ (Gz Sim) | Jazzy는 신규 Gazebo 호환 |
| Manipulation | ✓ | ✓ | O | 지원 시작 (2025 Q4~) |
| Home Service Challenge | ✓ | △ | X | Noetic 특화 콘텐츠 (Humble은 커스텀 필요) |
| Autonomous Driving | ✓ | ✓ | ✓ | 차선 인식 등 Jazzy 포팅 완료 |
| Machine Learning | X | △ | O | ROS 2 전용 ML 패키지 연동 |

💡 주요 변경 사항 및 설치 가이드
   * 1. ROS 2 Jazzy Jalisco (Ubuntu 24.04)
      •	현재 상황: 2026년 기준, 터틀봇3의 가장 표준이 되는 최신 버전입니다.
      •	특징: 이미지 속 "Soon" 단계에서 벗어나 **Manipulation(매니퓰레이션)**과 Machine Learning(기계 학습) 예제들이 공식 지원됩니다. 특히 Docker 컨테이너를 통한 배포가 안정화되어 라즈베리 파이 5에서도 원활하게 구동됩니다.
   * 2. ROS 2 Humble Hawksbill (Ubuntu 22.04)
      •	현재 상황: 가장 견고한 LTS(Long Term Support) 버전입니다.
      •	특징: 기업이나 연구실에서 '절대 안 죽는 환경'을 원할 때 여전히 1순위로 선택됩니다. 대부분의 시뮬레이션 환경이 이 버전에 최적화되어 있습니다.
   * 3. ROS 1 Noetic (지원 종료 알림)
      •	주의: 2025년 5월부로 공식 지원이 종료되었습니다. Home Service Challenge와 같은 과거의 특정 대회용 소스코드가 꼭 필요한 경우가 아니라면, 신규 설치 시에는 고려하지 않는 것이 좋습니다.

🛠️ 추천 환경 (Best Practice)
   * 만약 지금 라즈베리 파이에 새로 설치하신다면 아래 조합을 강력 추천합니다.
      •	하드웨어: Raspberry Pi 4 (4GB/8GB) 또는 Raspberry Pi 5
      •	OS: Ubuntu 24.04 LTS (64-bit)
      •	ROS 버전: ROS 2 Jazzy (Docker 활용 시 호환성 문제 해결이 가장 쉬움)


📋 기호별 의미 및 상태 설명
| 기호 | 의미 | 상태 설명 | 
|:-------:|:-------:|:-------:| 
| $\text{O}$ / $\checkmark$ | 공식 지원 (Full Support) |  제조사(ROBOTIS)의 공식 매뉴얼과 GitHub 소스코드가 완벽히 제공되며, 별도의 코드 수정 없이 즉시 구동 가능한 상태입니다. | 
| $\triangle$ | 부분 지원 (Partial / Beta) | 기본 기능은 동작하지만 일부 고급 기능이 빠져 있거나, 공식 배포판(Binary)이 아닌 소스 코드를 직접 빌드하여 사용해야 하는 '베타' 상태를 의미합니다.| 
| $\text{X}$ |  지원 불가 (Not Supported) | 해당 환경에서 구동하기 위한 패키지가 개발되지 않았거나, 의존성 문제로 인해 설치 및 실행이 불가능한 상태입니다.| 

🔍 주요 항목별 부연 설명
   * $\text{O}$ (Machine Learning - Jazzy):
      * 기존에는 ROS 2에서 ML 패키지 연동이 까다로웠으나, Jazzy 버전에서는 micro-ROS와 TensorFlow Lite 등의 연동 예제가 공식화되어 '지원($\text{O}$)'으로 표시했습니다.
   * $\triangle$ (Home Service Challenge - Humble):
      * 이 기능은 ROS 1 Noetic에 최적화된 시나리오입니다. Humble에서도 구동은 가능하지만, 사용자가 직접 맵과 명령 체계를 ROS 2용으로 컨버팅해야 하는 번거로움이 있어 '부분 지원'으로 분류됩니다.
   * $\text{X}$ (Manipulation - Jazzy 초기 단계):
      * 질문하신 시점의 최신 상태에 따라 다르지만, 일반적으로 최신 OS가 나오면 하드웨어 제어 라이브러리(Dynamixel SDK 등)가 포팅되는 데 시간이 걸립니다. 현재는 개발이 완료되어 $\text{O}$로 넘어가고 있는 추세입니다.


----

# 🖥️ Raspberry Pi 4 — Ubuntu 22.04 LTS Server + XRDP + XFCE4 GUI 환경 구성

Windows PC의 **MobaXterm**에서 **RDP**로 라즈베리파이 4의 **XFCE4 데스크탑**에 접속하는 완성 가이드입니다.

---

## 📋 전체 흐름

```
Ubuntu 22.04 Server 이미지 굽기
        ↓
초기 부팅 & SSH 접속
        ↓
시스템 업데이트
        ↓
XFCE4 데스크탑 설치
        ↓
XRDP 설치 & 설정
        ↓
MobaXterm RDP 접속
        ↓
✅ GUI 데스크탑 완성
```

---

## 🛠️ 개발 환경

| 항목 | 내용 |
|------|------|
| 하드웨어 | Raspberry Pi 4 |
| OS | Ubuntu 22.04 LTS Server (64-bit) |
| 데스크탑 환경 | XFCE4 |
| 원격 접속 서버 | XRDP (Port 3389) |
| 클라이언트 도구 | MobaXterm (Windows) |

---

## STEP 1. Ubuntu 22.04 LTS Server 이미지 설치

### 필요 도구

- **Raspberry Pi Imager** : https://www.raspberrypi.com/software/
- MicroSD 카드 (32GB 이상 권장)

### OS 선택

```
Other general-purpose OS → Ubuntu → Ubuntu Server 22.04 LTS (64-bit)
```

### ⚙️ 고급 설정 (톱니바퀴 아이콘)

이미지 굽기 전에 반드시 설정합니다.

```
☑ Set hostname:          rpi4
☑ Enable SSH:            Use password authentication
☑ Set username/password: [계정명] / [비밀번호]
☑ Configure wireless LAN: (Wi-Fi 사용 시 SSID/PW 입력)
☑ Set locale:            Asia/Seoul / ko_KR
```

> 이 설정을 완료하면 첫 부팅부터 바로 SSH 접속이 가능합니다.

---

## STEP 2. 라즈베리파이 부팅 & SSH 접속

### IP 주소 확인

공유기 관리 페이지에서 확인하거나, 모니터 직접 연결 후 아래 명령 실행:

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

## STEP 4. XFCE4 데스크탑 환경 설치

```bash
# XFCE4 설치 (경량 데스크탑 환경)
sudo apt install -y xfce4 xfce4-goodies
```

> 설치 중 **display manager 선택 팝업**이 나타나면 `lightdm` 을 선택합니다.

- `xfce4-goodies` : 파일 매니저, 텍스트 에디터 등 유틸리티 포함

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

접속 시 **색상 관리 인증 팝업 오류**가 반복되는 현상을 방지합니다.

```bash
sudo nano /etc/polkit-1/localauthority/50-local.d/xrdp-color.pkla
```

아래 내용을 붙여넣기합니다:

```ini
[Allow Colord for XRDP]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
```

```bash
# 저장: Ctrl+O → Enter → Ctrl+X
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

---

## STEP 8. 시스템 업데이트 완료

첫 접속 시 **Update Notifier 팝업**이 표시됩니다.  
터미널에서 직접 처리하는 것을 권장합니다:

```bash
sudo apt update && sudo apt full-upgrade -y
sudo reboot
```

재부팅 후 RDP로 다시 접속하면 **최종 완성 상태**입니다.

---

## 🔧 트러블슈팅

| 증상 | 원인 | 해결 방법 |
|------|------|-----------|
| 접속 후 회색 빈 화면 | `~/.xsession` 파일 없음 | `echo "xfce4-session" > ~/.xsession` 실행 |
| 포트 연결 거부 | xrdp 서비스 미실행 | `sudo systemctl start xrdp` |
| 로그인 후 바로 끊김 | 기존 SSH 세션 충돌 | SSH에서 먼저 로그아웃 후 RDP 접속 |
| 화면 깨짐 / 해상도 이상 | 해상도 불일치 | MobaXterm RDP 설정에서 해상도 수동 조정 |
| 색상 인증 팝업 반복 | polkit 설정 없음 | STEP 6 의 pkla 파일 생성 |

---

## 📊 최종 구성 요약

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
│       └── ~/.xsession               │
└─────────────────────────────────────┘
```

---

## 📝 참고

- `~/.xsession` 파일의 `xfce4-session` 한 줄이 데스크탑 환경을 결정하는 **핵심 설정**입니다.
- XFCE4는 라즈베리파이 4에서 쾌적하게 동작하는 **경량 데스크탑 환경**입니다.
- XRDP는 Windows의 기본 원격 데스크탑(mstsc.exe)으로도 접속할 수 있습니다.

