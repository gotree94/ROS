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
   * Humble: ROBOTIS 공식 매뉴얼이 가장 완벽하게 대응하며, OpenCR과의 펌웨어 호환성이 가장 높습니다.

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
