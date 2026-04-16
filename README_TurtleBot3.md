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

<img src="rp4-ros-install\rp4-ros-install_003.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_004.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_005.png"> <br>
<img src="rp4-ros-install\rp4-ros-install_006.png"> <br>

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

📋 기호별 의미 및 상태 설명
| 기호 | 의미 | 상태 설명 | 
|:-------:|:-------:|:-------:| 
| $\text{O}$ / $\checkmark$ | 공식 지원 (Full Support) |  제조사(ROBOTIS)의 공식 매뉴얼과 GitHub 소스코드가 완벽히 제공되며, 별도의 코드 수정 없이 즉시 구동 가능한 상태입니다. | 
| $\triangle$ | 부분 지원 (Partial / Beta) | 기본 기능은 동작하지만 일부 고급 기능이 빠져 있거나, 공식 배포판(Binary)이 아닌 소스 코드를 직접 빌드하여 사용해야 하는 '베타' 상태를 의미합니다.| 
| $\text{X}$ |  지원 불가 (Not Supported) | 해당 환경에서 구동하기 위한 패키지가 개발되지 않았거나, 의존성 문제로 인해 설치 및 실행이 불가능한 상태입니다.| 

💡 주요 변경 사항 및 설치 가이드
1. ROS 2 Jazzy Jalisco (Ubuntu 24.04)
•	현재 상황: 2026년 기준, 터틀봇3의 가장 표준이 되는 최신 버전입니다.
•	특징: 이미지 속 "Soon" 단계에서 벗어나 **Manipulation(매니퓰레이션)**과 Machine Learning(기계 학습) 예제들이 공식 지원됩니다. 특히 Docker 컨테이너를 통한 배포가 안정화되어 라즈베리 파이 5에서도 원활하게 구동됩니다.
2. ROS 2 Humble Hawksbill (Ubuntu 22.04)
•	현재 상황: 가장 견고한 LTS(Long Term Support) 버전입니다.
•	특징: 기업이나 연구실에서 '절대 안 죽는 환경'을 원할 때 여전히 1순위로 선택됩니다. 대부분의 시뮬레이션 환경이 이 버전에 최적화되어 있습니다.
3. ROS 1 Noetic (지원 종료 알림)
•	주의: 2025년 5월부로 공식 지원이 종료되었습니다. Home Service Challenge와 같은 과거의 특정 대회용 소스코드가 꼭 필요한 경우가 아니라면, 신규 설치 시에는 고려하지 않는 것이 좋습니다.
🛠️ 추천 환경 (Best Practice)
만약 지금 라즈베리 파이에 새로 설치하신다면 아래 조합을 강력 추천합니다.
•	하드웨어: Raspberry Pi 4 (4GB/8GB) 또는 Raspberry Pi 5
•	OS: Ubuntu 24.04 LTS (64-bit)
•	ROS 버전: ROS 2 Jazzy (Docker 활용 시 호환성 문제 해결이 가장 쉬움)

----



