# CMOS & Custom Compiler Study Notes

**반도체 CMOS 소자 및 회로 동작 원리부터 Physical Design, Stick Diagram, 그리고 Custom Compiler 설계 과정**까지를 정리한 학습 자료 모음  
트랜지스터 동작의 물리적 이해에서부터 논리 게이트 설계, 레이아웃, 전류 특성에 이르기까지 **Front-end VLSI 설계 전반**을 포함

---

## 주요 내용

### 1. CMOS 기본 개념
- One-Chip 구성 요소 (수동 소자, 능동 소자, 배선, 기판)
- CMOS의 장점: 집적도 향상, 성능 및 전력 효율 개선, 경제성 확보
- VLSI(초대규모 집적회로): CPU, GPU, ASIC, FPGA 등

### 2. CMOS 트랜지스터 구조
- NMOS, PMOS의 동작 조건과 Body 연결
- 전자와 정공 이동 속도의 차이에 따른 **W/L 설계 고려**
- 기본 논리소자 구현: Inverter, NAND, NOR

### 3. 포화 전류 (IDS,sat)
- 식: $I_{D,sat} = \frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{GS}-V_{th})^2$
- PMOS는 이동도가 낮아 동일 전류 확보를 위해 **NMOS 대비 더 큰 폭(Width)** 필요
- W, L 조절을 통한 포화 전류 제어 방법

### 4. CMOS 게이트 설계 및 Stick Diagram
- Complementary 구조: Pull-up(PMOS), Pull-down(NMOS) 네트워크
- 설계 규칙: 직렬/병렬 배치 변환
- Stick Diagram을 통한 레이아웃 계획 및 인버터, NAND, NOR 구현

### 5. 트랜지스터 동작 이론
- **MOS 캐패시터 동작 모드**: 축적(Accumulation), 공핍(Depletion), 반전(Inversion)
- **nMOS 동작 영역**:
  - Cutoff, Linear, Saturation
- **채널 길이 변조 (Channel Length Modulation)**  
  - 포화 영역에서도 $V_{ds}$ 증가 시 채널 길이가 줄어 전류 증가
  - 수정된 포화 전류 모델: $(1+\lambda V_{ds})$ 포함
- **바디 효과 (Body Effect)**  
  - $V_{sb}$ > 0일 경우 문턱 전압 증가 → 전류 감소
  - 설계 시 바디를 GND/VDD에 연결하여 $V_{sb}=0$ 유지
- **정전용량**  
  - 게이트-채널 정전용량 $C_{gs}$  
  - 기생 정전용량 $C_{sb}, C_{db}$

---

## 요약 표

| 항목              | 영향 요소              | 특징                          |
|-------------------|------------------------|-------------------------------|
| I-V 특성          | $V_{gs}, V_{ds}, V_t$ | 세 가지 동작 영역 (Cutoff, Linear, Saturation) |
| 채널 길이 변조    | $\lambda$              | 포화 전류 미세 증가, 출력 저항 감소 |
| 바디 효과         | $V_{sb}, \gamma$       | 문턱 전압 상승, 전류 감소 |
| 속도 결정 요소    | 전류, 정전용량         | $I = C \cdot \frac{dV}{dt}$ |

---

## 정리 포인트
- CMOS는 단순한 스위치 모델을 넘어, **물리적 현상(이동도, 문턱 전압, 기생 효과 등)**을 고려해야 함
- W/L, 정전용량, 바디 효과 등은 **회로 성능과 전력, 면적**을 결정하는 핵심 파라미터
- Stick Diagram은 **회로 → 레이아웃**으로 이어지는 중요한 다리 역할
- 이러한 이해는 **ASIC/FPGA Front-end 설계와 Custom Compiler 개발**로 확장 가능
