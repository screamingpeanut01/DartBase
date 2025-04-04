# 2nd_week

# 통계학 2주차 정규과제

📌통계학 정규과제는 매주 정해진 분량의 『*데이터 분석가가 반드시 알아야 할 모든 것*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **Statistics_2nd_TIL**에 나열된 분량을 읽고 `학습 목표`에 맞게 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 추가자료와 교재를 다시 참고하여 보완하는 것이 좋습니다.

2주차는 `1부. 데이터 기초체력 기르기`를 읽고 새롭게 배운 내용을 정리해주시면 됩니다.

## Statistics_2nd_TIL

### 1부. 데이터 기초체력 기르기

### 06. 확률분포

### 07. 가설검정

## Study Schedule

| 주차 | 공부 범위 | 완료 여부 |
| --- | --- | --- |
| 1주차 | 1부 p.2~56 | ✅ |
| 2주차 | 1부 p.57~79 | ✅ |
| 3주차 | 2부 p.82~120 | 🍽️ |
| 4주차 | 2부 p.121~202 | 🍽️ |
| 5주차 | 2부 p.203~254 | 🍽️ |
| 6주차 | 3부 p.300~356 | 🍽️ |
| 7주차 | 3부 p.357~615 | 🍽️ |

# **06. 확률분포 (Probability Distribution)**

확률분포란 확률변수가 가질 수 있는 값들과 그 값들이 발생할 확률 간의 관계를 나타내는 수학적 표현이다. 데이터 분석이나 머신러닝 모델을 설계할 때, 변수들의 분포 특성을 이해하는 것은 모델 선택 및 성능 향상에 중요한 역할을 한다. 특히 통계 분석에서는 이론적 분포를 통해 실제 데이터를 추정하거나 예측하게 되므로, 확률분포에 대한 개념은 데이터 과학의 기초 체력이라 할 수 있다.

## 6.1 확률분포의 정의와 종류

- **확률분포(Probability Distribution)**: 확률변수가 특정한 값을 가질 확률을 수학적으로 나타낸 함수
- **분류 기준**: 확률변수의 성격에 따라 이산/연속 분포로 나뉨
    - **이산 확률분포 (Discrete)**: 값이 셀 수 있는 경우 (예: 주사위, 동전)
    - **연속 확률분포 (Continuous)**: 값이 연속적인 구간에 걸쳐 있는 경우 (예: 키, 몸무게)

## 6.2 이산 확률분포

이산 확률분포는 결과값이 셀 수 있는 경우에 사용하며, 대표적인 분포로 균등분포, 이항분포, 초기하분포, 포아송분포가 있다.

### (1) 균등분포 (Uniform Distribution)

- 모든 결과값이 동등한 확률을 가지는 분포
- 예: 완벽한 주사위는 각 눈금(1~6)이 동일 확률(1/6)을 가짐
- 난수 생성 테스트 시 기준으로 삼기 좋음

### (2) 이항분포 (Binomial Distribution)

- 성공/실패 두 결과 중 하나가 나오는 시행을 n번 반복했을 때, 성공 횟수에 대한 분포
- 전제 조건:
    - 각 시행은 서로 독립
    - 성공 확률 p는 일정
- 예: 동전을 10번 던져 앞면이 나오는 횟수
- A/B 테스트, 마케팅 전환율 예측 등에 유용함

### (3) 초기하분포 (Hypergeometric Distribution)

- 복원 추출이 아닌 경우(추출 후 반환하지 않는 경우)에 사용하는 분포
- 예: 카드덱에서 특정 카드를 뽑을 확률
- 모집단이 작거나 복원되지 않는 샘플링 상황에서 중요함

### (4) 포아송분포 (Poisson Distribution)

- 단위 시간/공간당 사건이 몇 번 발생하는지를 모델링
- 예: 콜센터에 시간당 전화가 걸려오는 횟수
- 평균 발생률 λ가 핵심
- 이벤트 발생 예측, 서버 요청 횟수 분석 등에 사용

## 6.3 연속 확률분포

연속 확률분포는 확률변수가 연속적인 실수 값을 가질 때 사용하며, 대표적인 분포는 정규분포와 지수분포이다.

### (1) 정규분포 (Normal Distribution)

- 종 모양의 대칭형 분포로, 대부분의 자연현상과 사회현상이 따름
- 평균(μ)을 중심으로 대칭, 표준편차(σ)는 퍼짐 정도를 결정
- 예: 키, 시험 점수, 기온 등
- 표준화(Z-점수)를 통해 다른 분포와 비교하거나 이상치 탐지에 매우 유용

### (2) 지수분포 (Exponential Distribution)

- 사건 간 시간 간격을 모델링
- 포아송 분포와 관련 깊음 (포아송: 단위 시간 내 발생 횟수 / 지수: 사건 간 시간)
- 예: 고장 간격, 서버 요청 간 시간 등
- 평균 간격을 기준으로 확률 추정 시 효과적

## 6.4 중심극한정리 (Central Limit Theorem, CLT)

- **정의**: 임의의 모집단으로부터 크기 n인 표본을 반복 추출할 경우, n이 충분히 크면(일반적으로 n≥30) 표본평균의 분포는 정규분포를 따른다.
- **의의**:
    - 모집단 분포가 정규가 아니어도 정규 근사를 가능케 하여 통계적 추론을 정당화함
    - 표본평균의 신뢰구간 설정, 가설검정 등에 기반 이론
- **실전 팁**:
    - 표본 수가 적은 경우에는 t-분포 사용 필요
    - 이상치가 많은 데이터는 중심극한정리가 더디게 수렴할 수 있음

# **07. 가설검정 (Hypothesis Testing)**

가설검정은 통계적 추론에서 가장 핵심적인 절차 중 하나로, 어떤 주장(가설)이 데이터를 통해 통계적으로 유의미한지를 검정하는 방법이다.

## 7.1 귀무가설과 대립가설

- **귀무가설(H₀)**: 변화 없음, 차이 없음의 입장
- **대립가설(H₁)**: 변화 있음, 차이 있음의 입장
- 예:
    - H₀: 신약은 기존 약과 효과 차이 없음
    - H₁: 신약은 기존 약보다 효과 다름
- H₀는 '의심 대상'이 아니라, 기본값(default)으로 생각해야 함
- 실험 설계 시, H₁에 관심이 있지만 증명해야 할 대상은 H₀임

## 7.2 가설검정 절차

1. **가설 설정**: H₀과 H₁을 명확히 설정 (양측 or 단측 검정 여부 포함)
2. **검정통계량 계산**: z, t, χ² 등 데이터에 맞는 검정통계량 선택
3. **유의수준(α) 설정**: 일반적으로 0.05 사용, 보수적일 경우 0.01
4. **기각 기준 비교**: p-value나 임계값과 비교하여 H₀ 기각 여부 결정

## 7.3 유의수준과 p-value

- **유의수준 (α)**: H₀가 참일 때 잘못 기각할 확률 (1종 오류 확률)
- **p-value**: H₀가 참이라는 전제하에 현재 관측된 결과 이상의 극단적 데이터가 나올 확률
- 판단 기준:
    - p < α → H₀ 기각 (통계적으로 유의함)
    - p ≥ α → H₀ 채택 (유의하지 않음)
- **주의점**: p-value는 효과의 크기나 중요도를 말해주지 않음. 오직 “우연히 발생했을 가능성”만 말함.

### 7.4 1종 오류와 2종 오류

- **1종 오류 (Type I Error)**: H₀가 참인데 기각 (False Positive)
- **2종 오류 (Type II Error)**: H₁이 참인데 H₀를 기각하지 않음 (False Negative)
- **검정력 (Power)**: 1 - β, 2종 오류를 범하지 않을 확률 → 효과를 실제로 검출할 수 있는 능력

| 실제 \ 판단 | H₀ 채택 | H₀ 기각 |
| --- | --- | --- |
| H₀ 참 | 정확 | 1종 오류 |
| H₁ 참 | 2종 오류 | 정확 |
- 1종 오류가 더 중요할 경우(예: 암 진단), α를 낮춰야 함
- 2종 오류가 더 중요할 경우(예: 신약 효과 놓치기), 표본 수를 늘리거나 검정력을 높여야 함

## 문제 1.

> 🧚Q. 다음 중 귀무가설(H₀)을 기각해야 하는 경우는 언제인가요? 정답을 고르고, 그 이유를 간단히 설명해주세요.
> 

> 1️⃣ 유의수준(α)이 0.05이고, p값이 0.03일 때
2️⃣ 유의수준(α)이 0.01이고, p값이 0.02일 때
> 

```
p값은 귀무가설이 맞다고 했을 때, 지금 같은 결과가 나올 확률인데,
그 확률이 유의수준보다 작다는 건 ‘우연이라 보기 어렵다’는 뜻이므로 기각
```

### 🎉 수고하셨습니다.