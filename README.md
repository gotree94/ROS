# TurtleBot3 Burger — 심화 ROS 교육 커리큘럼

* 24주 (6개월) · 중급 입문 (임베디드/Linux 경험자) · Arduino → ROS 2 → Gazebo → Unreal Engine 5 → 멀티로봇 협업

## 전체로드랩

# 📚 Robotics & ROS 2 Advanced Curriculum (24 Weeks)

## Phase 1: HW 심화 & 통신 프로토콜 (주 1–3)

| Module | Topic | Details |
|--------|------|--------|
| M1-1 | Arduino 심화 & 펌웨어 | * 인터럽트 / 타이머 / DMA 개념<br> * FreeRTOS 태스크 구조<br>* 커스텀 UART 프로토콜 설계<br> * OpenCR 펌웨어 분석 & 수정 |
| M1-2 | 통신 프로토콜 실습 | * I2C/SPI 멀티 센서 버스 설계<br>* CAN 통신 개념 (산업 로봇 연계)<br>* Bluetooth / Wi-Fi 모듈 연동<br>* 패킷 구조 설계 & CRC 검증 |
| M1-3 | Raspberry Pi 심화 | * Device Tree / GPIO IRQ<br>* V4L2 카메라 드라이버 커스텀<br>* 실시간 커널 패치 (RT-PREEMPT)<br>Docker 기반 ROS 2 환경 격리 |

---

## Phase 2: ROS 2 Humble 심화 (주 4–8)

| Module | Topic | Details |
|--------|------|--------|
| M2-1 | ROS 2 아키텍처 & DDS | DDS (Fast-DDS / Cyclone DDS) 설정<br>QoS 정책 설계 (Reliability, Durability)<br>Executor / callback group 최적화<br>Lifecycle Node & 상태 관리 |
| M2-2 | C++ 노드 개발 | rclcpp 심화: 타이머 / 파라미터<br>커스텀 msg / srv / action 정의<br>Composable Node & intra-process<br>ROS 2 시간 동기화 (use_sim_time) |
| M2-3 | TF2 & 센서 통합 | 정적/동적 TF 브로드캐스터<br>URDF / Xacro 로봇 모델링<br>sensor_msgs 완전 활용<br>robot_state_publisher 구성 |
| M2-4 | Nav2 고급 설정 | 커스텀 플래너 / 컨트롤러 플러그인<br>behavior_tree_cpp v4 설계<br>Dynamic waypoint following<br>Costmap2D 레이어 커스터마이징 |
| M2-5 | SLAM & 위치 추정 | SLAM Toolbox lifetime mapping<br>AMCL / EKFB pose estimation<br>3D LiDAR 기초 (HDL/NDT SLAM)<br>Localization 정밀도 튜닝 |

---

## Phase 3: 컴퓨터 비전 & AI 통합 (주 9–12)

| Module | Topic | Details |
|--------|------|--------|
| M3-1 | OpenCV & 비전 파이프라인 | 카메라 캘리브레이션 (체스보드)<br>ArUco / AprilTag 마커 인식<br>깊이 추정 & 스테레오 비전<br>image_pipeline ROS 2 통합 |
| M3-2 | YOLOv8 & 객체 탐지 | YOLOv8 커스텀 학습 파이프라인<br>TensorRT / ONNX 최적화<br>ROS 2 vision_msgs 통합<br>RPi5 NPU 추론 가속 |
| M3-3 | 의미론적 내비게이션 | 객체 인식 → 목적지 결정<br>의미 지도 (semantic map) 구축<br>open_clip 이미지-언어 매칭<br>LLM 명령어 → ROS 2 action |
| M3-4 | 데이터셋 & 학습 환경 | 시뮬 합성 데이터 생성 자동화<br>38가지 이미지 증강 파이프라인<br>Roboflow / Label Studio 연동<br>지속 학습 (Continual Learning) 개요 |

---

## Phase 4: Gazebo Ignition 심화 시뮬레이션 (주 13–16)

| Module | Topic | Details |
|--------|------|--------|
| M4-1 | Gazebo 고급 환경 구축 | SDF v1.9 완전 정복<br>PBR 재질 / 광원 설정<br>복잡 지형 (계단 · 경사 · 문)<br>물리 엔진 튜닝 (DART / Bullet) |
| M4-2 | ros2_control & 하드웨어 추상화 | HardwareInterface 커스텀 작성<br>diff_drive_controller 심화<br>MoveIt 2 기초 연동<br>시뮬 → 실물 파라미터 이전 |
| M4-3 | 강화학습 환경 (Sim2Real) | gym_ros2 / IsaacGym 개요<br>PPO 기반 이동 정책 학습<br>도메인 랜덤화 자동화<br>실물 전이 검증 절차 |
| M4-4 | 다중 로봇 Gazebo 시뮬 | 5-TB3 동시 시뮬레이션<br>collision avoidance 벤치마크<br>분산 맵 병합 (map_merge_3d)<br>시뮬 성능 프로파일링 |

---

## Phase 5: Unreal Engine 5 + ROS 2 디지털 트윈 (주 17–20)

| Module | Topic | Details |
|--------|------|--------|
| M5-1 | UE5 C++ 기초 | AActor / UActorComponent 구조<br>UPROPERTY / UFUNCTION 매크로<br>Tick & 물리 시뮬레이션<br>Blueprint ↔ C++ 혼용 패턴 |
| M5-2 | rclUE & ROS 2 브리지 | rclUE 플러그인 빌드 & 설정<br>Topic / Service / Action 연동<br>TB3 URDF → UE5 스켈레탈 메시<br>센서 시뮬 (LiDAR · 카메라 렌더) |
| M5-3 | 고품질 디지털 트윈 | Lumen GI / Nanite 설정<br>실환경 3D 스캔 임포트 (RealityCapture)<br>합성 학습 데이터 대량 생성<br>실시간 로봇 상태 시각화 |
| M5-4 | UE5 멀티로봇 시각화 | 다중 에이전트 상태 동기화<br>Fleet 관제 HUD 설계<br>이벤트 기반 알림 시스템<br>WebSocket ↔ ROS 2 브리지 |

---

## Phase 6: 멀티로봇 협업 & 시스템 통합 (주 21–22)

| Module | Topic | Details |
|--------|------|--------|
| M6-1 | 멀티에이전트 ROS 2 | ROS 2 namespace & domain 분리<br>중앙 조율 노드 아키텍처<br>Task allocation (경매 알고리즘)<br>Fleet management (Open-RMF 개요) |
| M6-2 | 분산 SLAM & 지도 공유 | 로봇 간 지도 공유 프로토콜<br>맵 병합 & 일관성 유지<br>공유 Costmap 설계<br>통신 지연 보상 기법 |
| M6-3 | 산업 인터페이스 연동 | MQTT / OPC-UA 브리지<br>PLC ↔ ROS 2 통신<br>스마트 팩토리 시나리오 설계<br>안전 기능 (e-stop, watchdog) |

---

## Phase 7: 캡스톤 프로젝트 & 포트폴리오 (주 23–24)

| Module | Topic | Details |
|--------|------|--------|
| M7-1 | 팀 시스템 통합 | 전체 스택 통합 디버깅<br>실제 TB3 + UE5 동시 데모<br>성능 벤치마크 & 튜닝<br>장애 대응 시나리오 테스트 |
| M7-2 | 포트폴리오 완성 | GitHub README 전문 작성<br>데모 영상 편집 & 업로드<br>기술 블로그 포스트 작성<br>최종 발표 (15분 + Q&A) |

## 주차별 상세(24주)

# 📅 24주 로보틱스 & ROS 2 커리큘럼 로드맵

| 주차 | 주제 | 핵심 실습 | 결과물 / 마일스톤 |
|------|------|----------|------------------|
| 1주 | Arduino 심화 & OpenCR 펌웨어 (Phase 1 — HW 심화) | 인터럽트·타이머·DMA 실습<br>OpenCR 펌웨어 분석 & 수정 | 커스텀 OpenCR 펌웨어 동작 |
| 2주 | 통신 프로토콜 설계 (Phase 1) | I2C 멀티 센서 버스<br>커스텀 UART 패킷 구조 설계 & CRC 검증 | 센서 허브 프로토타입 |
| 3주 | RPi 심화 & Docker 환경 (Phase 1) | V4L2 카메라 드라이버<br>RT-PREEMPT<br>Docker ROS 2 컨테이너 | 컨테이너화된 ROS 2 환경 |
| 4주 | ROS 2 아키텍처 & DDS 설정 (Phase 2 — ROS 2 심화) | Fast-DDS QoS 정책 실험<br>Lifecycle Node 상태 다이어그램 | QoS 비교 벤치마크 보고서 |
| 5주 | C++ 노드 & 커스텀 인터페이스 (Phase 2) | rclcpp Composable Node<br>커스텀 msg/srv/action 패키지 작성 | 재사용 가능한 인터페이스 패키지 |
| 6주 | TF2 & URDF 로봇 모델링 (Phase 2) | Xacro 매크로 TB3 확장<br>동적 TF 브로드캐스터 | 커스텀 URDF 모델 + RViz2 시각화 |
| 7주 | SLAM Toolbox & 위치 추정 (Phase 2) | Lifelong mapping<br>AMCL 튜닝<br>EKF 포즈 퓨전 | 지속 맵 + 위치 오차 분석 |
| 8주 | Nav2 고급 & BehaviorTree (Phase 2) | 커스텀 플래너 플러그인<br>BT XML 설계<br>Dynamic waypoint | 자율 순찰 데모 (5 waypoint) |
| 9주 | 카메라 캘리브레이션 & ArUco (Phase 3 — 비전+AI) | 체스보드 캘리브레이션<br>ArUco 6x6 마커 위치 추정 | 마커 기반 도킹 보조 시스템 |
| 10주 | YOLOv8 커스텀 학습 (Phase 3) | 데이터셋 수집→증강→학습<br>TensorRT 변환 | 실시간 객체 탐지 ROS 2 노드 |
| 11주 | 의미론적 내비게이션 (Phase 3) | 객체 인식 → 목적지 결정<br>Semantic map 구축 | "빨간 박스 앞으로 이동" 시연 |
| 12주 | LLM → ROS 2 명령 파이프라인 (Phase 3 ★중간발표) | 자연어 → action goal 변환<br>합성 데이터 자동 생성 | 중간 발표: 비전+AI 통합 데모 |
| 13주 | Gazebo 고급 환경 & SDF (Phase 4 — Gazebo 심화) | PBR 재질<br>계단·경사 지형 구성<br>물리 엔진 튜닝 | 실내 창고 시뮬 월드 |
| 14주 | ros2_control & MoveIt 2 (Phase 4) | HardwareInterface 커스텀<br>diff_drive_controller 심화 | 시뮬 ↔ 실물 동일 제어 |
| 15주 | 강화학습 환경 구축 (Phase 4) | gym_ros2 래핑<br>PPO 정책 학습<br>도메인 랜덤화 | RL 이동 정책 검증 |
| 16주 | 5-TB3 멀티로봇 Gazebo (Phase 4) | 5대 동시 시뮬<br>map_merge<br>충돌 회피 벤치마크 | 멀티로봇 탐색 시뮬 영상 |
| 17주 | UE5 C++ 기초 & Actor (Phase 5 — UE5+ROS) | AActor/Component 구조<br>Tick 최적화<br>BP↔C++ 혼용 | UE5 하이브리드 액터 |
| 18주 | rclUE 브리지 구축 (Phase 5) | rclUE 빌드<br>Topic/Action 연동<br>TB3 UE5 임포트 | UE5 내 TB3 원격 제어 |
| 19주 | 고품질 디지털 트윈 (Phase 5) | Lumen/Nanite<br>3D 스캔 임포트<br>합성 데이터 생성 | 디지털 트윈 환경 완성 |
| 20주 | UE5 멀티로봇 Fleet HUD (Phase 5 ★UE5발표) | 상태 동기화<br>Fleet HUD 설계<br>WebSocket 브리지 | UE5 발표: 관제 시연 |
| 21주 | 멀티에이전트 ROS 2 조율 (Phase 6 — 멀티로봇) | 경매 기반 Task allocation<br>namespace 설계 | 3-TB3 자동 배분 시연 |
| 22주 | 산업 인터페이스 & 안전 (Phase 6) | MQTT/OPC-UA 브리지<br>PLC 연동<br>e-stop/watchdog | 스마트 팩토리 프로토타입 |
| 23주 | 캡스톤 — 시스템 통합 (Phase 7 — 캡스톤) | 전체 스택 통합<br>TB3+UE5 실시간 연동<br>성능 튜닝 | 최종 시스템 완성 (95%+) |
| 24주 | 최종 발표 & 포트폴리오 (Phase 7) | README 작성<br>데모 영상 제작<br>기술 블로그 | 공개 GitHub 포트폴리오 |

## 5대 프로젝트

# 🚀 Projects Portfolio

| 프로젝트 | 설명 | 사용 기술 | 결과물 | 난이도 |
|----------|------|----------|--------|--------|
| P1 🗺️ 자율 탐사 & 의미론적 내비게이션 로봇 | LiDAR SLAM으로 미지 공간을 탐색하고 YOLOv8 객체 인식으로 의미 기반 목표 설정. LLM 자연어 명령(예: "파란 의자 옆에 대기")을 ROS 2 Action으로 변환하여 자율 이동 수행. BehaviorTree 기반 미션 흐름 제어 | SLAM Toolbox<br>Nav2<br>YOLOv8<br>BehaviorTree<br>LLM | 12주 결과물 | 개인 · 고급 |
| P2 🏭 Gazebo + UE5 물류 창고 디지털 트윈 | 실제 창고 환경을 Gazebo와 UE5에 동시 모델링. TB3가 바코드 인식 → 선반 픽업 → 배송 수행. UE5 Lumen 기반 시각화 및 센서 렌더링, 합성 데이터 자동 생성 파이프라인 포함 | Gazebo<br>Unreal Engine 5<br>rclUE<br>YOLOv8<br>Nav2 | 20주 결과물 | 팀(2인) · 고급 |
| P3 🤖 강화학습 기반 자율 이동 정책 (Sim2Real) | Gazebo gym 환경에서 PPO로 장애물 회피 및 목표 도달 정책 학습. 도메인 랜덤화 적용으로 실환경 전이 성능 향상. 실제 TB3에서 정책 검증 및 성능 비교 | PPO<br>gym_ros2<br>Domain Randomization<br>TensorRT | 16주 결과물 | 개인 · 고급 |
| P4 🚦 3-TB3 협업 스마트 팩토리 자동화 | 3대 TurtleBot이 경매 기반 Task allocation으로 작업 분배. MQTT 기반 PLC 신호 연동, 분산 맵 공유 및 충돌 회피. UE5 Fleet HUD로 실시간 관제 | Open-RMF<br>MQTT<br>UE5 HUD<br>Multi-Robot<br>Nav2 | 22주 결과물 | 팀(3인) · 최고급 |
| P5 📡 지능형 실내 배달 & 이상 탐지 시스템 | 병원/스마트빌딩 환경에서 자율 배달 수행. YOLOv8 기반 낙상/장애물 탐지 시 Telegram 알림 전송. ROS 2 Action 기반 상태 관리 및 웹 대시보드 제공 | YOLOv8<br>Telegram Bot<br>Flask<br>Nav2 Action<br>WebSocket | 캡스톤 | 팀(2인) · 중고급 |


## 장비·툴·평가

# 🛠️ Hardware

| 항목 | 설명 |
|------|------|
| TurtleBot3 Burger × 3 | 멀티로봇 실습용 |
| Arduino Mega / Nano | 펌웨어 · 프로토콜 실습 |
| Raspberry Pi 4/5 | 온보드 컴퓨터 |
| OpenCR 1.0 | 모터 드라이버 + IMU |
| LDS-02 LiDAR | 360° 2D 스캔 |
| Intel RealSense D435 | RGB-D 깊이 카메라 |
| GPU 워크스테이션 | RTX 3070+ (UE5 / 학습) |
| Wi-Fi 6 공유기 | 멀티로봇 통신 인프라 |

---

# 💻 Software Stack

| 항목 | 설명 |
|------|------|
| Ubuntu 22.04 LTS | 기본 개발 환경 |
| RT-PREEMPT 커널 | 실시간 처리 지원 |
| ROS 2 Humble | LTS · Nav2 · ros2_control |
| Gazebo Ignition Fortress | 로봇 시뮬레이션 |
| Unreal Engine 5.3+ | 디지털 트윈 · rclUE |
| YOLOv8 / Ultralytics | 객체 탐지 · TensorRT 최적화 |
| OpenCV 4.x | 이미지 처리 파이프라인 |
| Docker / Compose | 환경 격리 · CI/CD |
| Git + GitHub Actions | 협업 · 자동화 테스트 |
| VS Code + ROS Extension | 개발 환경 · colcon 통합 |
| MQTT / OPC-UA | 산업 인터페이스 연동 |

---

# 📊 Evaluation Criteria

| 항목 | 비율 | 설명 |
|------|------|------|
| 주간 실습 과제 | 35% | 매주 GitHub 제출 (README + 동작 캡처 포함) |
| 중간 발표 (12주) | 15% | 비전 + 내비 통합 개인 데모 (RViz2 영상 제출) |
| UE5 데모 (20주) | 15% | 디지털 트윈 + ROS 2 연동 시연 |
| 팀 캡스톤 (24주) | 25% | 실제 TB3 + 시뮬 통합 (5분 데모 + 발표) |
| 포트폴리오 | 10% | GitHub 공개 레포 + 기술 블로그 |

