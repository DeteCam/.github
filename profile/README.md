# DeteCam — WiFi 송출형 초소형 카메라 탐지 및 위치 추정

한국공학대학교 컴퓨터공학 졸업작품입니다. 방 안의 여러 전자기기 가운데 WiFi로 영상을 보내는 숨은 카메라만 골라내고, 그 방향을 스마트폰 AR로 보여 주는 것이 목표입니다.

## 목표

| 목표 | 합격 기준 (실측) |
|---|---|
| 카메라만 골라내기 | 재현율 95% 이상, 오탐률 5% 이하 (실제 기기, 기기 단위로 나눠 평가) |
| 방향 오차 줄이기 | 사람이 많고 반사가 있는 방에서, 같은 날 같은 자리에서 잰 DiffLoc 재현보다 평균 방향 오차 3° 이상 작게 |
| AR 표시 | 의심 구역이 실제 카메라를 포함하는 비율 90% 이상 |

제약: 움직이는 부품 없음(소음 없음) · 부품 값 70만 원 미만 · 사용자가 돌아다니지 않음 · PCB 외주 없음 · 쇼핑몰 기성품 · 사기 전에 검증.

## 현재 방향 — 움직이지 않는 스위치 고리 수신기

- 지름 9~10 cm 원 위에 막대 안테나 8개를 세우고 기성 RF 스위치 모듈로 번갈아 연결합니다. 기준 안테나 1개와 함께 Intel AX210의 두 수신 단자로 받아 패킷마다 생기는 위상 오차를 지웁니다.
- 정확도는 소프트웨어 · AI로 올립니다: 벽 · 천장 반사를 넣은 방향 추정, 위치를 아는 송신기로 하는 현장 보정, 신뢰도로 못 믿을 측정 거르기, 실제 트래픽으로 학습하는 카메라 판별.
- 아직 실측 결과는 없습니다. 지금까지의 숫자는 모두 시뮬레이션이며, 설계 선택의 근거로만 씁니다.

## 저장소

| 저장소 | 담는 것 |
|---|---|
| [docs](https://github.com/DeteCam/docs) | 작업 기준서 `AGENTS.md`, 원칙, 시스템 스펙, 주제 설명서, 구매 부품 목록, 기술 검증 보고서 |
| [receiver](https://github.com/DeteCam/receiver) | 스위치 고리 수신기 스펙, 시뮬레이션 코드(`sim/`). 지난 v6 설계는 `archive/v6-nano2` 브랜치에 보관 |
| [ai](https://github.com/DeteCam/ai) | 카메라 판별, 반사를 반영한 방향 추정 스펙과 설계 |
| [app](https://github.com/DeteCam/app) | 수신기 조종과 AR 표시 앱 스펙, 주소 계약 |
| [receiver-legacy](https://github.com/DeteCam/receiver-legacy) | 구형 42 cm 스탠드(v4) 보관 *(읽기 전용)* |

작업 규칙은 [CONTRIBUTING.md](https://github.com/DeteCam/.github/blob/main/CONTRIBUTING.md)와 [AGENTS.md](https://github.com/DeteCam/docs/blob/main/AGENTS.md)를 따릅니다.
