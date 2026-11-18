<div align="center">

<img src="assets/banner.png" alt="DeteCam — Wi-Fi 송출형 초소형 카메라 탐지 및 위치 추정 시스템" width="100%">

### 숨어서 영상을 내보내는 Wi-Fi 카메라를 찾아, 어디에 있는지 짚어 주는 시스템

![상태](https://img.shields.io/badge/상태-설계·사전_검증_끝,_시제품_준비-19C2B0?style=flat-square)
![대상](https://img.shields.io/badge/대상-Wi--Fi_송출_카메라-10304F?style=flat-square)
![수신기](https://img.shields.io/badge/수신기-ESP32--C5_패널_+_Raspberry_Pi-E7352C?style=flat-square&logo=espressif&logoColor=white)
![앱](https://img.shields.io/badge/앱-Android_·_ARCore-3DDC84?style=flat-square&logo=android&logoColor=white)
![AI](https://img.shields.io/badge/AI-PyTorch_·_Sionna_RT-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)

**[▶ 동작 영상](https://detecam.github.io/receiver/videos/)** &nbsp;·&nbsp; **[작품 범위](https://github.com/DeteCam/receiver/blob/main/docs/%EC%9E%91%ED%92%88%20%EB%B2%94%EC%9C%84.md)** &nbsp;·&nbsp; **[설계도](https://github.com/DeteCam/receiver/blob/main/docs/%EC%84%A4%EA%B3%84%EB%8F%84.md)** &nbsp;·&nbsp; **[데모 환경](https://github.com/DeteCam/receiver/blob/main/docs/%EB%8D%B0%EB%AA%A8%20%ED%99%98%EA%B2%BD.md)** &nbsp;·&nbsp; **[사전 검증](https://github.com/DeteCam/receiver/blob/main/docs/%EC%82%AC%EC%A0%84%20%EA%B2%80%EC%A6%9D.md)**

</div>

## DeteCam 은

숙소의 몰래카메라, 그리고 시험지를 찍어 밖으로 보내는 초소형 카메라. 둘 다 **찍은 것을 Wi-Fi 로 내보낸다**는 점이 같습니다. 지금 파는 탐지기는 "근처에 전파가 있다"까지만 알려 주고, 어디에 있는지는 사람이 구석구석 대 봐야 압니다. 시험 중에는 그마저 할 수 없습니다. 시험장의 와이파이를 끊어도 카메라는 폰 핫스팟이나 LTE 로 우회하고, 전파 방해(재밍)는 법으로 막혀 있습니다. 그래서 끊지 않고 찾습니다.

DeteCam 은 둘레의 Wi-Fi 를 엿들어 **카메라처럼 보내는 기기를 가려내고**, 벽에 걸어 둔 안테나 패널로 그 전파가 오는 **방향을 재서 자리를 짚고**, 그 자리를 **폰 화면 속 방 위에 겹쳐** 보여 줍니다. 모터가 없어 조용하고, 한 번 재는 데 0.3초입니다.

![시스템 구성도](https://raw.githubusercontent.com/DeteCam/receiver/main/docs/images/%EC%84%A4%EA%B3%84%EB%8F%84_%EC%8B%9C%EC%8A%A4%ED%85%9C_%EA%B5%AC%EC%84%B1.png)

## 이렇게 찾습니다

| | 하는 일 | 어떻게 |
|---|---|---|
| 🔎 **가려내기** | 둘레의 기기 가운데 카메라를 골라 MAC 주소를 알아낸다 | 암호화돼 있어도 프레임의 주소·길이·간격은 보인다. 영상을 올리는 기기의 무늬로 '의심 점수'를 매긴다 |
| 📡 **짚기** | 그 기기가 보낼 때마다 방향을 재고, 두 방향이 만나는 곳을 자리로 낸다 | 안테나 16개 패널이 안테나를 바꿔 가며 세기만 재서 위상을 되찾는다. 전송이 올 때마다 쌓아 좁힌다 |
| 📱 **보여 주기** | 의심 자리 세 곳을 확률과 함께 폰 화면에 띄운다 | 패널의 AR 마커를 폰으로 비춰 좌표를 맞춘다 (ARCore) |

## 계산으로 본 결과

전파 경로 계산(Sionna RT)으로 본 숫자입니다. 실물 시제품은 지금 만들고 있습니다.

| 상황 | 결과 |
|---|---|
| 40석 강의실, 패널 둘을 마주 보는 벽에 걸어 둠 | 앱이 띄우는 의심 좌석 3곳 안에 사진 4장이면 96%, 16장이면 99% 든다 (정확한 자리는 81%, 92%). 그 자리나 옆자리는 한 번 보내면 85~94%, 네 번이면 93~99% (책상 위 · 가슴 · 안경). 가장 약한 곳은 뒤쪽 창가 자리다 ([배치 계산](https://github.com/DeteCam/receiver/blob/main/docs/%EB%B0%B0%EC%B9%98%20%EA%B3%84%EC%82%B0.md)) |
| 숙소 방 (3.6 × 5.4 m, 욕실 포함), 패널 하나 | 방 가운데에서 다섯 쪽으로 돌려 재면 숨긴 카메라와 0.26 m (가운데값), 두 곳에서 더 재면 0.21 m |
| 실물의 흔들림을 넣어도 | 이득 2 dB, 위상 20도가 흔들려도 옆자리까지 맞힌 비율이 4점 안에서 버틴다 |

## 데모

<table>
<tr>
<td width="50%"><img src="https://raw.githubusercontent.com/DeteCam/receiver/main/docs/images/%EB%8D%B0%EB%AA%A8_%ED%99%98%EA%B2%BD_%EA%B5%90%EC%8B%A4.png" alt="강의실 데모"></td>
<td width="50%"><img src="https://raw.githubusercontent.com/DeteCam/receiver/main/docs/images/%EB%8D%B0%EB%AA%A8_%ED%99%98%EA%B2%BD_%EB%B0%A9.png" alt="숙소 방 데모"></td>
</tr>
<tr>
<td><b>강의실</b> · 패널 둘을 걸어 두고, 자리에 둔 카메라를 찾는다</td>
<td><b>숙소 방</b> · 패널 하나로 네 자리에서 재서, 숨긴 카메라를 찾는다</td>
</tr>
</table>

## 저장소

| | 저장소 | 담은 것 | 지금 |
|---|---|---|---|
| 📡 | [**receiver**](https://github.com/DeteCam/receiver) | 수신기: 패널과 허브의 3D 모델과 출력 파일, 장치 코드, 전파 시뮬레이션, 설계도와 데모 환경 | 설계 · 계산 검증 끝, 부품 관문 1 |
| 📱 | [**app**](https://github.com/DeteCam/app) | 안드로이드 앱: 수신기 조종, 패널 자리 등록, 의심 자리 AR 표시 | 스펙 |
| 🧠 | [**ai**](https://github.com/DeteCam/ai) | 의심 점수 모델(카메라 가려내기), 자리 모델(물리 계산 × 배운 모델) | 스펙 · 규칙 기준선 |
| 📚 | [**docs**](https://github.com/DeteCam/docs) | 원칙, 시스템 명세, 시스템 설계서, 조사, 검증 요약 | 계속 고침 |
| 🗄️ | [**receiver-legacy**](https://github.com/DeteCam/receiver-legacy) | 앞선 구조(알루미늄 판을 돌려 방향을 재는 수신기)의 모든 것 | 보관 (비공개) |

## 지금 어디까지 왔나

- [x] 구조를 정했다: 판을 돌리는 수신기에서 안테나 패널로 바꿈 ([설계 검토](https://github.com/DeteCam/receiver/blob/main/docs/%EC%84%A4%EA%B3%84%20%EA%B2%80%ED%86%A0.md)). 앞선 구조는 [receiver-legacy](https://github.com/DeteCam/receiver-legacy) 에 보관
- [x] 3D 모델, 출력 파일(G코드), 조립 영상
- [x] 부품을 사기 전의 검증: 공개된 시험 보고, 가진 기록의 분석, 흔들림을 넣은 계산 ([사전 검증](https://github.com/DeteCam/receiver/blob/main/docs/%EC%82%AC%EC%A0%84%20%EA%B2%80%EC%A6%9D.md))
- [x] 범위를 확정했다 (2026-11-19): 2.4 · 5 GHz Wi-Fi 카메라의 탐지와 자리, 두 대역 패널 둘. 이동통신 · 블루투스는 확장 과제 ([작품 범위](https://github.com/DeteCam/receiver/blob/main/docs/%EC%9E%91%ED%92%88%20%EB%B2%94%EC%9C%84.md))
- [x] 숙소 방에서 숨긴 카메라 찾기 계산 ([숙소 방 계산](https://github.com/DeteCam/receiver/blob/main/docs/%EC%88%99%EC%86%8C%20%EB%B0%A9%20%EA%B3%84%EC%82%B0.md))
- [ ] 부품 관문 1~5: 싼 것부터 사서 확인하고 다음 것을 산다 (3만 → 7.9만 → 5.3만 → 25.7만 → 41.3만 원, 모두 약 83만 원, 지원 100~150만 원)
- [ ] 패널 장치 코드, 허브 코드, 앱, 배운 모델
- [ ] 강의실과 숙소 방 데모

## 찾는 것과 찾지 못하는 것

| 범위 | 무엇 |
|---|---|
| **작품** | 2.4 · 5 GHz Wi-Fi 로 사진이나 영상을 보내는 카메라 전부 (사진을 간간이 보내든, 실시간으로 보내든, 버튼을 누를 때만 보내든). 공공 와이파이 · 폰 핫스팟 · 카메라 자체 AP · 숨긴 네트워크 어디에 붙었든 탐지 → 카메라 판별 → 자리 → AR 표시. 시험장은 의심 좌석 3곳, 숙소 방은 50 cm 안팎 |
| **패널** | 직접 만드는 두 대역(2.4 · 5 GHz) 판 둘. 두 대역 카메라 모두 같은 기준으로 자리를 잰다 |
| **확장 과제 (있다만)** | 근처 블루투스(BLE) 기기가 있다는 것과 대수 (허브 내장, 0원), 교실 안 휴대폰의 LTE 송신 경보 (RTL-SDR). 자리는 모른다. 작품이 된 뒤 시간이 남으면 |
| **범위 밖** | 전파 방해(재밍), 통신 내용 풀기, LTE · 5G · 블루투스 기기의 자리, 블루투스 클래식, 저장만 하는 카메라 (SD 카드), 유선 · 자기 유도 이어폰 |

까닭과 지금 설계로 되는지는 [작품 범위](https://github.com/DeteCam/receiver/blob/main/docs/%EC%9E%91%ED%92%88%20%EB%B2%94%EC%9C%84.md)에 있습니다.

## 함께 만드는 방식

- **스펙부터 씁니다.** 저장소마다 `specs/번호-이름/` 에 `spec.md`(무엇을, 왜) → `plan.md`(어떻게) → `tasks.md`(할 일)를 쓰고 만듭니다. 원칙과 시스템 명세는 [docs](https://github.com/DeteCam/docs) 에 있습니다.
- **계산과 실측을 가릅니다.** 숫자마다 시뮬레이션인지 실물로 잰 것인지 적습니다.
- **규칙**: 커밋 제목, 브랜치, PR, 이슈는 [CONTRIBUTING](https://github.com/DeteCam/.github/blob/main/CONTRIBUTING.md) 을 따릅니다.

<sub>한국공학대학교 컴퓨터공학부 종합설계 (2026~2027)</sub>
