# 🤖 로봇 산업 분류 총정리 (Robot Industry Taxonomy)

> 로봇 유형 · 산업 분류 · 하드웨어 · 소프트웨어 전체 체계 정리

---

## 📌 목차

1. [로봇 유형 분류](#1-로봇-유형-분류)
2. [산업 분야별 분류](#2-산업-분야별-분류)
3. [하드웨어 분류](#3-하드웨어-분류)
4. [소프트웨어 분류](#4-소프트웨어-분류)
5. [전체 구조 요약](#5-전체-구조-요약)

---

## 1. 로봇 유형 분류

### 1.1 형태·목적 기반 분류

| 대분류 | 소분류 | 설명 | 주요 제품 / 기업 |
|--------|--------|------|-----------------|
| **휴머노이드** | 이족보행 로봇 | 인간과 유사한 이족 구조, 범용 작업 | Boston Dynamics Atlas, Tesla Optimus, Figure 01, Unitree H1 |
| **휴머노이드** | 상반신 로봇 | 상체만 인간형, 고정 베이스 | Apptronik Apollo(상체), Agility Digit |
| **산업용 로봇** | 수직 다관절 | 6축 이상 관절, 용접·조립·도장 | FANUC, KUKA, ABB, Yaskawa |
| **산업용 로봇** | 수평 다관절 (SCARA) | 고속 수평 동작, 조립·픽앤플레이스 | Epson, Yamaha, Omron |
| **산업용 로봇** | 델타 로봇 | 병렬 구조, 초고속 소물 픽킹 | ABB FlexPicker, Fanuc M-1 |
| **산업용 로봇** | 협동 로봇 (Cobot) | 인간과 공간 공유, 안전 우선 | Universal Robots, Doosan, Hanwha |
| **이동 로봇** | AGV (Autonomous Guided Vehicle) | 고정 경로 추종 (마그네틱·QR·라인) | Daifuku, Toyota L&F, Hyster-Yale |
| **이동 로봇** | AMR (Autonomous Mobile Robot) | 자율 경로 계획, SLAM 기반 | MiR, Locus, Geek+, Cainiao |
| **이동 로봇** | 사족보행 로봇 | 험지 주행, 검사·순찰 | Boston Dynamics Spot, Unitree Go2 |
| **이동 로봇** | 드론 (UAV) | 항공 이동, 물류·측량·방위 | DJI, Skydio, Zipline |
| **이동 로봇** | 수중 로봇 (AUV/ROV) | 수중 탐사·점검 | Saab Seaeye, Ocean Infinity |
| **서비스 로봇** | 배송 로봇 | 실내·외 자율 배송 | Starship, Nuro, Bear Robotics |
| **서비스 로봇** | 의료 로봇 | 수술·재활·간호 보조 | Intuitive Surgical (da Vinci), Stryker |
| **서비스 로봇** | 청소 로봇 | 자율 청소·방역 | iRobot, Gaussian, Avidbots |
| **서비스 로봇** | 교육·소셜 로봇 | 감정 인식, 인터랙션 | SoftBank Pepper, NAVER ARC |
| **특수 목적 로봇** | 군사·방산 로봇 | 정찰·폭발물 처리·화력 지원 | QinetiQ TALON, Ghost Robotics |
| **특수 목적 로봇** | 우주 로봇 | 행성 탐사·궤도 작업 | NASA Mars Rover, JAXA |
| **특수 목적 로봇** | 농업 로봇 | 파종·수확·방제 자동화 | John Deere, Naïo Technologies |

---

## 2. 산업 분야별 분류

| 산업 분야 | 주요 적용 로봇 | 핵심 기능 | 대표 기업 |
|-----------|---------------|-----------|-----------|
| **제조 / 스마트팩토리** | 산업용 다관절, Cobot | 용접, 조립, 도장, 검사 | FANUC, KUKA, Hyundai Robotics |
| **물류 / 창고** | AGV, AMR, 피킹 로봇 | 입출고, 분류, 피킹, 팔레타이징 | Amazon Robotics, MiR, Geek+ |
| **의료 / 헬스케어** | 수술 로봇, 재활 로봇 | 최소침습수술, 재활치료, 원격진료 | Intuitive, Stryker, Renishaw |
| **농업 / 식품** | 농업 로봇, 식품 자동화 | 수확, 선별, 포장, 방제 | Soft Robotics, Octinion |
| **건설 / 인프라** | 용접 로봇, 검사 드론 | 구조물 점검, 용접, 3D 프린팅 | Built Robotics, Boston Dynamics |
| **국방 / 보안** | 무인 지상차량, 드론 | 정찰, 폭발물 처리, 경계 | Textron, Ghost Robotics |
| **서비스 / 유통** | 서비스 로봇, 배송 로봇 | 안내, 서빙, 주문, 배달 | Bear Robotics, Starship |
| **에너지 / 플랜트** | 검사 로봇, 수중 ROV | 파이프라인 점검, 설비 유지보수 | Aker Solutions, Oceaneering |
| **우주 / 항공** | 우주 탐사 로봇, 조립 로봇 | 탐사, 실험, 무인 조립 | NASA JPL, ESA |
| **교육 / 연구** | 교육용 플랫폼, 연구 로봇 | 프로그래밍 교육, 알고리즘 연구 | ROBOTIS TurtleBot, LEGO Mindstorms |

---

## 3. 하드웨어 분류

### 3.1 구동계 (Actuator & Drive)

| 분류 | 세부 항목 | 설명 | 주요 제품 / 기업 |
|------|-----------|------|-----------------|
| **모터** | BLDC 모터 | 브러시리스 DC, 고효율·고속 | Maxon, Faulhaber, T-Motor |
| **모터** | 서보 모터 | 위치·속도·토크 정밀 제어 | Yaskawa Σ-7, Panasonic MINAS |
| **모터** | 스테퍼 모터 | 오픈루프 위치 제어, 저가 구성 | Leadshine, Oriental Motor |
| **모터** | 리니어 모터 | 직선 운동, 백래시 없음 | Hiwin, Parker |
| **모터** | 유압·공압 액추에이터 | 고출력 힘 제어 (인간형 다리 등) | Moog, Parker Hannifin |
| **감속기** | 하모닉 드라이브 | 초정밀·고감속비, 백래시 제로 | Harmonic Drive Systems, HDSI |
| **감속기** | 사이클로이드 감속기 | 고토크·충격 내구성 | Nabtesco, Sumitomo |
| **감속기** | 유성 감속기 | 컴팩트·중간 감속비 | Neugart, SEW-Eurodrive |
| **감속기** | 직결 구동 (Direct Drive) | 감속기 없음, 역구동성 우수 | Robodrive, T-Motor |
| **모터 드라이버** | EtherCAT 드라이버 | 산업용 실시간 통신 서보 드라이버 | Beckhoff, Elmo, Kollmorgen |
| **모터 드라이버** | CAN/CANopen 드라이버 | 로봇 관절 네트워크 표준 | PEAK System, iMotion |
| **모터 드라이버** | FOC 드라이버 | 벡터 제어, BLDC/PMSM용 | ODrive, VESC, SimpleMotion |
| **모터 드라이버** | 마이크로스텝 드라이버 | 스테퍼 정밀 제어 | Trinamic (TMC), Gecko |

### 3.2 센서 (Sensor)

| 분류 | 세부 항목 | 설명 | 주요 제품 / 기업 |
|------|-----------|------|-----------------|
| **위치·자세** | 인코더 (절대/증분) | 관절 각도·속도 측정 | Renishaw, Heidenhain, Broadcom |
| **위치·자세** | IMU (관성센서) | 가속도·자이로·자세 측정 | Bosch BMI088, VectorNav, ADIS |
| **위치·자세** | 힘/토크 센서 | 말단장치 접촉력 측정 | ATI, OnRobot, Bota Systems |
| **거리·공간** | LiDAR | 3D 점군, SLAM·내비게이션 | Velodyne, Ouster, Livox, RPLIDAR |
| **거리·공간** | 깊이 카메라 (RGB-D) | 구조광·ToF 기반 3D 인식 | Intel RealSense, Microsoft Azure Kinect |
| **거리·공간** | 초음파 센서 | 단거리 장애물 감지 | MaxBotix, Murata |
| **거리·공간** | 레이더 (mmWave) | 악천후·먼지 환경 감지 | Texas Instruments IWR, Infineon |
| **비전** | 2D 산업 카메라 | 비전 검사, 마커 인식 | Basler, FLIR, Sony IMX |
| **비전** | 이벤트 카메라 | 고속·저지연 동적 감지 | Prophesee, inivation |
| **환경** | 온도·습도 | 환경 모니터링 | Sensirion, TE Connectivity |
| **촉각** | 촉각 센서 (Tactile) | 파지력·슬립 감지 | SynTouch, Xela Robotics |

### 3.3 제어기 및 컴퓨팅 (Controller & Computing)

| 분류 | 세부 항목 | 설명 | 주요 제품 / 기업 |
|------|-----------|------|-----------------|
| **산업용 제어기** | PLC | 시퀀스·I/O 제어, 산업 표준 | Siemens S7, Allen-Bradley, Mitsubishi |
| **산업용 제어기** | 로봇 전용 컨트롤러 | 관절 통합 제어, OEM 제공 | FANUC R-30iB, KUKA KRC5 |
| **임베디드 컴퓨터** | ARM 마이크로컨트롤러 | 저수준 실시간 제어 | STM32, NXP i.MX RT, RP2040 |
| **임베디드 컴퓨터** | SBC (싱글보드컴퓨터) | ROS 상위 제어, 비전 처리 | Raspberry Pi 4/5, NVIDIA Jetson Orin |
| **임베디드 컴퓨터** | 산업용 PC (IPC) | 고성능 실시간 연산 | Beckhoff IPC, Kontron |
| **AI 가속기** | GPU 모듈 | 딥러닝 추론·학습 | NVIDIA Jetson AGX, Intel NCS2 |
| **AI 가속기** | NPU / FPGA | 엣지 AI 추론, 저전력 | Xilinx Kria, Intel Agilex, Hailo |
| **통신** | EtherCAT | 실시간 산업 이더넷 | Beckhoff, Acontis |
| **통신** | CAN / CANopen | 관절·센서 네트워크 | Kvaser, Peak |
| **통신** | ROS 2 DDS (UDP) | 소프트웨어 레이어 통신 | Fast DDS, Cyclone DDS |
| **전원** | SMPS / BMS | 전원 공급·배터리 관리 | Texas Instruments, Victron |

### 3.4 메커니즘 및 구조 (Mechanism & Structure)

| 분류 | 세부 항목 | 설명 |
|------|-----------|------|
| **엔드이펙터** | 병렬 그리퍼 | 가장 일반적, 단단한 물체 파지 |
| **엔드이펙터** | 3손가락 그리퍼 | 복잡 형상 파지, 인간 유사 |
| **엔드이펙터** | 진공 석션 | 편평·대면적 물체, 고속 픽킹 |
| **엔드이펙터** | 소프트 그리퍼 | 연성 재질, 취약물 파지 |
| **엔드이펙터** | 용접·도장 툴 | 용접건, 스프레이 건 |
| **링크 구조** | 직렬 링크 | 일반 다관절 로봇, 넓은 작업공간 |
| **링크 구조** | 병렬 링크 | 델타, 스튜어트 플랫폼, 고강성 |
| **이동 플랫폼** | 차동 구동 | 2휠, 단순 구조, AMR 기본 |
| **이동 플랫폼** | 옴니휠 | 전방향 이동, 좁은 공간 |
| **이동 플랫폼** | 메카넘휠 | 전방향, 산업용 AGV |
| **이동 플랫폼** | 트랙 구동 | 험지·계단 주행 |

---

## 4. 소프트웨어 분류

### 4.1 미들웨어 및 프레임워크

| 분류 | 세부 항목 | 설명 | 주요 도구 |
|------|-----------|------|-----------|
| **로봇 OS** | ROS 1 (Noetic) | 레거시, 연구용 여전히 사용 | Ubuntu 20.04 기반, EOL 2025 |
| **로봇 OS** | ROS 2 (Humble/Iron/Jazzy) | 실시간·보안·멀티로봇 지원 | Humble LTS (2027), Fast DDS |
| **로봇 OS** | ROS 2 + micro-ROS | 마이크로컨트롤러용 ROS 2 | STM32, ESP32 지원 |
| **통신 미들웨어** | DDS (Data Distribution Service) | ROS 2 기반 통신 레이어 | Fast DDS, Cyclone DDS, RTI Connext |
| **통신 미들웨어** | MQTT / AMQP | IoT·클라우드 연결, 경량 | Eclipse Mosquitto, RabbitMQ |
| **통신 미들웨어** | OPC-UA | 스마트팩토리 표준 통신 | Unified Automation, open62541 |

### 4.2 인식 및 AI 소프트웨어

| 분류 | 세부 항목 | 설명 | 주요 도구 |
|------|-----------|------|-----------|
| **SLAM** | LiDAR SLAM | 레이저 기반 지도 생성·위치 추정 | Cartographer, SLAM Toolbox, LIO-SAM |
| **SLAM** | Visual SLAM | 카메라 기반 SLAM | ORB-SLAM3, RTAB-Map, OpenVINS |
| **SLAM** | 융합 SLAM | LiDAR + IMU + 카메라 | LIO-SAM, FAST-LIO2 |
| **내비게이션** | 경로 계획 | 전역·지역 경로 생성 | Nav2 (ROS2), MoveBase, Dijkstra/A* |
| **내비게이션** | 장애물 회피 | 동적 장애물 실시간 회피 | DWA, TEB, VFH |
| **컴퓨터 비전** | 객체 인식 | 딥러닝 기반 2D/3D 물체 감지 | YOLOv8, Ultralytics, OpenCV |
| **컴퓨터 비전** | 포즈 추정 | 물체·사람 자세 추정 | MediaPipe, FoundationPose, DOPE |
| **컴퓨터 비전** | 포인트클라우드 처리 | 3D 점군 분류·분할 | PCL, Open3D, PointNet++ |
| **조작 AI** | 모방 학습 (IL) | 시연 데이터로 정책 학습 | ACT, Diffusion Policy, BC-Z |
| **조작 AI** | 강화학습 (RL) | 시뮬레이션 보상 기반 학습 | Isaac Lab, MuJoCo, Stable-Baselines3 |
| **조작 AI** | 기반 모델 (Foundation) | VLM·LLM 로봇 통합 | RT-2, OpenVLA, Octo |

### 4.3 제어 소프트웨어

| 분류 | 세부 항목 | 설명 | 주요 도구 |
|------|-----------|------|-----------|
| **운동학·동역학** | 순/역기구학 (FK/IK) | 관절각 ↔ 말단위치 변환 | KDL, IKFast, TRAC-IK, Pinocchio |
| **운동학·동역학** | 동역학 엔진 | 힘·토크·관성 계산 | Pinocchio, Featherstone, Drake |
| **궤적 계획** | 조인트 공간 계획 | 관절 각도 기반 궤적 | MoveIt2, Ruckig, TOPP-RA |
| **궤적 계획** | 작업 공간 계획 | 카테시안 공간 직선·원호 보간 | MoveIt2 Cartesian Planner |
| **저수준 제어** | PID 제어 | 위치·속도·토크 기본 피드백 | ros2_control, Arduino PID |
| **저수준 제어** | FOC / 벡터 제어 | BLDC 전류 벡터 실시간 제어 | ODrive, VESC firmware |
| **저수준 제어** | 임피던스 / 컴플라이언스 제어 | 힘·강성 기반 유연 접촉 제어 | ros2_control, Franka FCI |
| **저수준 제어** | RTOS 기반 제어 | 하드 실시간 실행 보장 | FreeRTOS, Zephyr, VxWorks |
| **고수준 제어** | 행동 트리 (Behavior Tree) | 태스크 상태 기계 관리 | BehaviorTree.CPP, Py-Trees |
| **고수준 제어** | 태스크 플래너 | 작업 순서·조건 계획 | PDDL, ROSPlan, Task and Motion Planning |

### 4.4 시뮬레이션

| 분류 | 세부 항목 | 설명 | 주요 도구 |
|------|-----------|------|-----------|
| **물리 시뮬레이터** | 범용 로봇 시뮬 | ROS 연동 표준 환경 | Gazebo (Classic / Ignition), Webots |
| **물리 시뮬레이터** | 고속 RL 시뮬 | GPU 병렬화, 대규모 학습 | NVIDIA Isaac Sim, MuJoCo, PyBullet |
| **물리 시뮬레이터** | 멀티바디 동역학 | 메커니즘 설계 검증 | Adams, RecurDyn, Simscape |
| **비전 시뮬레이터** | 합성 데이터 생성 | 학습용 이미지·점군 생성 | NVIDIA Isaac Replicator, BlenderProc |
| **디지털 트윈** | 실시간 연동 트윈 | 실물 ↔ 가상 실시간 동기화 | NVIDIA Omniverse, Azure Digital Twins |
| **디지털 트윈** | 공정 시뮬레이션 | 제조라인 최적화·분석 | Siemens Tecnomatix, Dassault DELMIA |
| **디지털 트윈** | ROS 2 연동 트윈 | 로봇 소프트웨어 레벨 통합 | Isaac ROS, ROS 2 + Omniverse |
| **시각화** | 로봇 상태 시각화 | 관절·센서·경로 3D 표시 | RViz2, Foxglove Studio |
| **시각화** | 3D 뷰어 (웹) | 브라우저 기반 Three.js 뷰어 | Three.js, Babylon.js, rerun.io |

### 4.5 개발 도구 및 인프라

| 분류 | 세부 항목 | 설명 | 주요 도구 |
|------|-----------|------|-----------|
| **펌웨어 개발** | 임베디드 IDE | 마이크로컨트롤러 펌웨어 개발 | STM32CubeIDE, PlatformIO, Keil MDK |
| **펌웨어 개발** | HAL / BSP | 하드웨어 추상화 레이어 | STM32 HAL, NXP SDK, Zephyr RTOS |
| **펌웨어 개발** | 실시간 디버깅 | JTAG/SWD 디버거 | J-Link, OpenOCD, STLink |
| **로봇 개발** | 빌드 시스템 | ROS 2 패키지 빌드 | colcon, ament_cmake, CMake |
| **로봇 개발** | 패키지 관리 | 의존성·배포 | rosdep, vcstool, pip |
| **로봇 개발** | 로깅·분석 | 센서 데이터 기록·재생 | ROS 2 bag, Foxglove, PlotJuggler |
| **DevOps** | 컨테이너화 | 환경 격리·배포 | Docker, ROS Docker Hub |
| **DevOps** | CI/CD | 자동 빌드·테스트 | GitHub Actions, Jenkins, GitLab CI |
| **DevOps** | 원격 모니터링 | 로봇 Fleet 관리 | AWS RoboMaker, FORT Robotics |

---

## 5. 전체 구조 요약

```
로봇 산업 (Robot Industry)
│
├── 로봇 유형
│   ├── 휴머노이드 (Humanoid)
│   ├── 산업용 로봇 (Industrial) ─ 다관절, SCARA, 델타, Cobot
│   ├── 이동 로봇 (Mobile) ──────── AGV, AMR, 사족보행, 드론, 수중
│   ├── 서비스 로봇 (Service) ───── 배송, 의료, 청소, 교육
│   └── 특수 목적 (Special) ─────── 군사, 우주, 농업
│
├── 산업 분야
│   ├── 제조 / 스마트팩토리
│   ├── 물류 / 창고
│   ├── 의료 / 헬스케어
│   ├── 농업 / 식품
│   ├── 건설 / 인프라
│   ├── 국방 / 보안
│   ├── 서비스 / 유통
│   └── 에너지 / 플랜트
│
├── 하드웨어
│   ├── 구동계 ─── 모터 (BLDC/서보/스테퍼) → 감속기 (하모닉/사이클로이드) → 모터 드라이버
│   ├── 센서 ──── LiDAR · RGB-D · IMU · 인코더 · 힘토크 · 비전
│   ├── 제어기 ── MCU (STM32) · SBC (Jetson/RPi) · IPC · AI 가속기
│   ├── 통신 ──── EtherCAT · CAN · DDS · MQTT · OPC-UA
│   └── 구조 ──── 엔드이펙터 · 링크 구조 · 이동 플랫폼
│
└── 소프트웨어
    ├── 미들웨어 ─── ROS 2 · micro-ROS · DDS · OPC-UA
    ├── 인식 AI ──── SLAM · 내비게이션 · 비전 · 조작 AI (RL/IL/VLM)
    ├── 제어 ──────── 운동학 · 궤적 계획 · PID · FOC · 임피던스 · BT
    ├── 시뮬레이션 ─ Gazebo · Isaac Sim · MuJoCo · 디지털 트윈
    └── 개발도구 ──── 펌웨어 IDE · colcon · ROS bag · Docker · CI/CD
```

---

## 참고 자료

- [ROS 2 Documentation](https://docs.ros.org/en/humble/)
- [NVIDIA Isaac Platform](https://developer.nvidia.com/isaac)
- [MoveIt 2](https://moveit.ros.org/)
- [ROBOTIS TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [Open Robotics](https://www.openrobotics.org/)

---

> **Author:** 나무 (광주인력개발원 임베디드·지능형 로봇 과정)
> **Last Updated:** 2026-04
