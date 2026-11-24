<div align="center">

<img src="assets/banner.png" alt="DeteCam 5.0 (Palm-12) — 손바닥 크기 벽면 부착형 Wi-Fi 초소형 카메라 탐지 및 위치 추정 시스템" width="100%">

### 손바닥 크기(`12 cm`) 벽면 부착·각도 조절 수신기 3기로 숨은 카메라를 찾아 짚어 주는 시스템

![버전](https://img.shields.io/badge/버전-DeteCam_5.0_(Palm--12)-19C2B0?style=flat-square)
![수신기](https://img.shields.io/badge/수신기-12cm_12%2B1소자_통합PCB_+_ROCK_3A/AX210-10304F?style=flat-square)
![출력](https://img.shields.io/badge/3D_출력-Bambu_X1C_단_1판_(4h52m,_서포트_0%25)-EB6834?style=flat-square)
![비용](https://img.shields.io/badge/3기_신품_총비용-약_46.7만_원_(-44%25)-0F766E?style=flat-square)

**[▶ 조립·동작 영상](https://detecam.github.io/receiver/videos/)** &nbsp;·&nbsp; **[주제 설명서](https://github.com/DeteCam/docs/blob/main/%EC%A3%BC%EC%A0%9C_%EC%84%A4%EB%AA%85%EC%84%9C.md)** &nbsp;·&nbsp; **[부품 목록](https://github.com/DeteCam/receiver/blob/main/docs/%EB%B6%80%ED%92%88_%EB%AA%A9%EB%A1%9D.md)** &nbsp;·&nbsp; **[3D 출력·조립](https://github.com/DeteCam/receiver/blob/main/docs/%EC%A1%B0%EB%A6%BD_%EB%B0%8F_%EC%B6%9C%EB%A0%A5_%EC%95%88%EB%82%B4.md)** &nbsp;·&nbsp; **[현장 최적배치(AR-OPA)](https://github.com/DeteCam/receiver/blob/main/docs/%ED%98%84%EC%9E%A5_%EC%B5%9C%EC%A0%81%EB%B0%B0%EC%B9%98_%EA%B0%80%EC%9D%B4%EB%93%9C.md)**

</div>

## DeteCam 5.0 (Palm-12)의 4대 혁신

1. **손바닥 크기 + 무타공 벽면 스위블**: 기존 42 cm 대형 L자 팔과 2.5 m 조명 스탠드를 없애고 **`120 × 120 × 30.6 mm` 손바닥 크기**로 축소했습니다. **네오디뮴 자석 4개(사물함·칠판) + 재사용 나노겔 패드(타일·거울·벽지)**로 손 닿는 벽면에 1초 부착한 뒤, 직교 2축 짐벌로 **좌우 `±30°` · 상하 `0°/-15°/-25°`** 각도만 딸깍 맞춥니다.
2. **더 작아졌는데 5 GHz는 오히려 100배 정확 + 비용 44% 절감**: 12+1소자 SMD 칩 안테나(`Abracon AANI-CH-0078`)·`PE42442 × 4`·`AD8317`을 **`112 × 112 mm` 4층 통합 RF PCB 1장**으로 통합하고 `Radxa ROCK 3A`(`VesperCSI` ARM64, 팬리스)를 채택해 3기 신품 총비용을 **약 84만 원 → 약 46.7만 원**으로 낮췄습니다. 소자 간격 `26.8 mm`로 5.2 GHz 부엽 `PSL 0.472`(`0.57°`)를 달성하고, 2.45 GHz 상호결합은 1회 턴테이블 보정 역행렬 `C⁻¹` + `CM-RCLPA`로 **`1.68°`**까지 복원합니다 `[시뮬레이션]`.
3. **교수님 2대 핵심 질문의 완벽한 해답**:
   - **수많은 기기 중 카메라만 선별**: 1단계 수동 무늬 → 2단계 **5초 조명 점멸/보행 인과 자극(`CamLoPA`)** → 3단계 **3D 방 경계 필터 + `AD8317×3` LTE/5G 교차 차감**.
   - **간섭·반사가 심한 실내 위치 추정**: MAC 분리 + `TriF v12` (`C⁻¹` 결합 보정 + `Capon` + `CV_f` 가중 + **10면 가상 거울 앵커** + **RAPS 90% 통계 보장 AR 구역**).
4. **어떤 공간에서도 20초 최적 배치 (`AR-OPA` + `Auto-Verify`)**: 숙소·화장실·목욕탕·탈의실·40석 교실·150석 강당 6대 실공간 시뮬레이션에서 입구 벽면 직부착 대비 최악 10% 오차(P90) **`-65.9%` 단축 (`4.22 m → 1.44 m`)**, 각도 고정 벽부착 대비 협소 3공간(화장실 `-29.8%` · 탈의실 `-20.0%` · 숙소 `-17.9%`) 추가 개선을 입증했습니다 `[시뮬레이션]`.

<div align="center">
  <img src="https://raw.githubusercontent.com/DeteCam/receiver/main/docs/images/palm12_wall_swivel.png" alt="Palm-12 벽면 부착 스위블" width="48%">
  <img src="https://raw.githubusercontent.com/DeteCam/receiver/main/docs/images/ar_opa_and_v5_benchmark.png" alt="AR-OPA 6공간 검증 및 Palm-12 비교" width="48%">
</div>

## 저장소 (v5.0 단일화 완료)

| | 저장소 | 담은 것 | 상태 |
|---|---|---|---|
| 📡 | [**receiver**](https://github.com/DeteCam/receiver) | Palm-12 CAD(`palm_node.py`), 무서포트 STL 6종, **Bambu X1C 단 1판 G코드**, `TriF v12`/`AR-OPA` 펌웨어(`pytest 5/5`), EM·6공간 시뮬레이션, 조립·동작 영상 | v5.0 설계·슬라이싱·검증 완료 |
| 📚 | [**docs**](https://github.com/DeteCam/docs) | 원칙(`constitution.md`), 주제 설명서, 기술검증 보고서, 시스템 스펙, **Figma Slides 바로 가져오기용 `.pptx` 발표자료** | v5.0 최신화 |
| 🧠 | [**ai**](https://github.com/DeteCam/ai) | 3단계 카메라 판별기, `TriF v12 + C⁻¹ + RAPS`, 벽면 스위블 `AR-OPA` 알고리즘 설계 및 스펙 | v5.0 최신화 |
| 📱 | [**app**](https://github.com/DeteCam/app) | 안드로이드 ARCore 앱 스펙 및 수신기 REST API 계약 (`주소 계약.md`) | v5.0 최신화 |
| 🗄️ | [**receiver-legacy**](https://github.com/DeteCam/receiver-legacy) | 초기 회전 반사판 방식(v1~v2) 보관 전용 | 보관 (수정 안 함) |

## 찾는 것과 한계 (숨기지 않는 원칙)

- **정밀 3D 위치 + 90% AR 구역**: 2.4 GHz 및 5 GHz Wi-Fi 송출형 초소형 카메라 전부 (공공 Wi-Fi · 핫스팟 · 숨김 SSID · 자체 AP).
- **존재·구역 경보 (확장)**: 유심 LTE/5G 몰래카메라 (`AD8317×3` 교차 차감 최근접 노드), BLE 카메라 (AX210 내장 Bluetooth 5.3 RSSI 구역, 0원).
- **범위 밖 (명시)**: 전파 방해(재밍), 통신 내용 복호화, 전원이 꺼졌거나 SD 카드에만 단독 저장하는 비송출 카메라.

<sub>한국공학대학교 컴퓨터공학부 종합설계 (2026~2027) · DeteCam 5.0 (Palm-12)</sub>
