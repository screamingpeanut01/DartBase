# 6th_week

# 통계학 6주차 정규과제

📌통계학 정규과제는 매주 정해진 분량의 『*데이터 분석가가 반드시 알아야 할 모든 것*』 을 읽고 학습하는 것입니다. 이번 주는 아래의 **Statistics_6th_TIL**에 나열된 분량을 읽고 `학습 목표`에 맞게 공부하시면 됩니다.

아래의 문제를 풀어보며 학습 내용을 점검하세요. 문제를 해결하는 과정에서 개념을 스스로 정리하고, 필요한 경우 추가자료와 교재를 다시 참고하여 보완하는 것이 좋습니다.

6주차는 `3부. 데이터 분석하기`를 읽고 새롭게 배운 내용을 정리해주시면 됩니다.

## Statistics_6th_TIL

### 3부. 데이터 분석하기

### 12.통계 기반 분석 방법론

## Study Schedule

| 주차 | 공부 범위 | 완료 여부 |
| --- | --- | --- |
| 1주차 | 1부 p.2~56 | ✅ |
| 2주차 | 1부 p.57~79 | ✅ |
| 3주차 | 2부 p.82~120 | ✅ |
| 4주차 | 2부 p.121~202 | ✅ |
| 5주차 | 2부 p.203~254 | ✅ |
| 6주차 | 3부 p.300~356 | ✅ |
| 7주차 | 3부 p.357~615 | 🍽️ |

## 분석 모델 개요

### 통계 모델과 기계 학습

데이터 분석 방법론은 크게 통계학에 기반한 통계 모델(Statistical Models)과 인공지능에서 파생된 *계 학습(Machine Learning)으로 나눌 수 있다.

- **통계 모델**: 모형과 해석을 중시하며, 데이터가 특정 확률 분포를 따른다고 가정하고 모수 추정을 통해 현상을 설명하거나 가설을 검정한다. 오차와 불확실성을 강조한다.
- **기계 학습**: 대용량 데이터를 활용하여 예측의 정확도를 높이는 데 중점을 둔다. 알고리즘을 통해 데이터로부터 패턴을 학습하고 예측이나 분류 성능을 최적화한다.

두 분야는 경계가 모호하고 상호 보완적이다. 기계 학습도 기본적으로 통계 모델의 원리를 기반으로 하므로, 대표적인 통계 모델 방법론을 제대로 익히는 것이 중요하다.

### 데이터 분석 방법론의 분류

기계 학습 방법론은 주로 종속변수의 유무와 변수의 속성(질적/양적 척도)에 따라 분류된다.

### 지도 학습 (Supervised Learning)

입력(독립변수)과 정답(종속변수)이 주어진 데이터를 사용하여 모델을 학습시키는 방법이다.

- **회귀 (Regression)**: 종속변수가 연속형(양적) 변수일 때 사용된다. (예: 주택 가격 예측)
    - 선형 회귀, 회귀 트리, 랜덤 포레스트 회귀, 신경망 등
- **분류 (Classification)**: 종속변수가 범주형(질적) 변수일 때 사용된다. (예: 스팸 메일 분류, 고객 이탈 예측)
    - 로지스틱 회귀, 분류 트리, 랜덤 포레스트 분류, 나이브 베이즈, 서포트 벡터 머신(SVM), k-최근접 이웃(k-NN), 신경망, 판별분석 등

### 비지도 학습 (Unsupervised Learning)

정답(종속변수) 없이 입력 데이터만으로 변수 간의 패턴을 파악하거나 데이터를 그룹화하는 방법이다.

- **차원 축소 (Dimensionality Reduction)**: 변수의 수를 줄여 데이터의 복잡성을 낮추고, 시각화나 다른 분석 모델의 성능 향상을 위해 사용된다.
    - 주성분 분석(PCA), 요인 분석(Factor Analysis)
- **군집 분석 (Clustering)**: 유사한 특성을 가진 데이터들을 그룹(군집)으로 묶는다. (예: 고객 세분화)
    - k-평균 군집(k-Means), 계층적 군집분석, Self-Organizing Map (SOM)
- **연관 규칙 (Association Rules)**: 데이터 항목들 간의 흥미로운 관계를 발견한다. (예: 장바구니 분석 - "맥주를 구매한 고객은 기저귀도 함께 구매하는 경향이 있다")
    - Apriori, FP-Growth

### 강화 학습 (Reinforcement Learning)

에이전트(agent)가 환경(environment)과 상호작용하며, 보상(reward)을 최대화하는 행동(action)을 학습하는 방법이다. (예: 게임 AI, 로봇 제어)

- Model-free RL, Model-based RL

## 주성분 분석 (PCA: Principal Component Analysis)

### PCA의 개념 및 목적

여러 개의 변수들 간에 존재하는 상관관계를 이용하여, 이 변수들의 정보를 최대한 유지하면서 서로 독립적인 새로운 변수(주성분)들을 찾아내는 기법이다. 주성분 분석을 통해 변수의 수를 줄여(차원 축소) 모형을 단순화하고 분석 결과를 효과적으로 해석할 수 있다.

### 차원의 저주 (Curse of Dimensionality)

변수(차원)의 수가 증가함에 따라 분석에 필요한 최소 데이터 건수가 기하급수적으로 늘어나고, 예측 성능이 저하되거나 과적합(overfitting)의 위험이 커지는 현상이다.

### PCA의 원리

데이터의 분산을 최대한 보존하는 새로운 축(주성분)을 찾는 것이 핵심이다.

1. 데이터 표준화 (각 변수의 평균을 0, 분산을 1로 만든다).
2. 공분산 행렬 또는 상관계수 행렬을 계산한다.
3. 고유값(eigenvalue)과 고유벡터(eigenvector)를 계산한다. 고유벡터가 주성분의 방향을, 고유값이 해당 주성분이 설명하는 분산의 크기를 나타낸다.
4. 고유값이 큰 순서대로 주성분을 선택한다. 제1주성분은 원 데이터의 분산을 가장 많이 설명하는 축이며, 제2주성분은 제1주성분과 직교하면서 나머지 분산을 가장 많이 설명하는 축이다.

### 주성분의 설명력

각 주성분의 고유값을 전체 고유값의 합으로 나눈 값으로, 해당 주성분이 전체 데이터 변동의 몇 %를 설명하는지를 나타낸다.

## 공통요인분석 (CFA: Common Factor Analysis / EFA: Exploratory Factor Analysis)

### 3.1. 요인분석의 개념 및 종류

여러 변수들 간의 상관관계를 바탕으로, 이 변수들 뒤에 잠재된 공통 요인(latent factor)을 찾아내어 변수들의 구조를 파악하고 변수의 수를 줄이는 분석 방법이다.

- **탐색적 요인분석 (EFA, Exploratory Factor Analysis)**: 변수와 요인 간의 관계가 사전에 정립되지 않은 상태에서 데이터로부터 요인 구조를 탐색적으로 발견하고자 할 때 사용된다. 본 문서에서는 주로 EFA를 다룬다.
- **확인적 요인분석 (CFA, Confirmatory Factor Analysis)**: 이론이나 선행 연구를 바탕으로 설정한 요인 구조 가설을 실제 데이터를 통해 통계적으로 검증하고 확인하고자 할 때 사용된다.

### PCA와 CFA(EFA)의 비교

| 구분 | 주성분 분석 (PCA) | 공통요인분석 (CFA/EFA) |
| --- | --- | --- |
| **목표** | 정보 손실 최소화, 차원 축소 | 변수 간 잠재 구조 파악, 공통 요인 추출 |
| **분산 활용** | 총 분산 (고유 분산 + 공통 분산 + 오차 분산) | 공통 분산 (변수들이 공유하는 분산) |
| **요인/성분** | 주성분들은 서로 독립적, 설명력 순으로 중요도 결정 | 요인들은 이론적 의미를 가지며, 반드시 중요도 순서는 아니다 |

실제로는 두 방법이 유사하게 사용되기도 하지만, CFA/EFA가 변수들 간의 기저 구조를 파악하는 데 더 적합하다고 알려져 있다.

### 요인분석의 적합성 검증

- **바틀렛(Bartlett)의 구형성 검정**: 변수들 간에 상관관계가 존재하여 요인분석에 적합한지를 검정한다. 귀무가설은 "상관행렬이 단위행렬이다(변수들이 독립적이다)". p-value < 0.05 이면 요인분석에 적합하다고 판단한다.
- **KMO (Kaiser-Meyer-Olkin) 표본 적합성 측도**: 변수들 간의 상관관계가 다른 변수에 의해 잘 설명되는 정도를 나타낸다. 일반적으로 0.5 이상이면 요인분석에 적합하다고 보며, 0.8 이상이면 매우 좋다고 판단한다.

### 요인의 수 결정

- **고유치 (Eigenvalue)**: 각 요인이 설명하는 분산의 양이다. 일반적으로 고유치가 1 이상인 요인들만 선택하는 카이저 기준(Kaiser's criterion)을 사용한다.
- **스크리 도표 (Scree Plot)**: 요인의 수에 따른 고유치의 변화를 시각화한 그래프이다. 그래프의 기울기가 완만해지기 시작하는 지점(엘보우 포인트, elbow point) 이전까지의 요인을 선택한다.
- **누적 설명 분산**: 선택된 요인들이 전체 분산의 일정 비율(예: 60% 이상)을 설명하는지 확인한다.

### 요인 적재값 (Factor Loading)

각 변수와 각 요인 간의 상관계수를 의미하며, 요인이 해당 변수를 얼마나 잘 설명하는지를 나타낸다. 절댓값이 클수록(보통 0.3 또는 0.5 이상) 해당 변수가 그 요인과 관련이 높다고 해석하며, 이를 통해 각 요인의 의미를 부여한다. 요인 회전(varimax 등)을 통해 요인 적재값의 해석을 용이하게 할 수 있다.

## 다중공선성 해결과 섀플리 밸류 분석

### 다중공선성 (Multicollinearity)

회귀분석에서 독립변수들 간에 높은 선형 관계가 나타나는 현상이다.

### 다중공선성의 문제점

- 회귀계수 추정치의 분산이 커져 불안정해진다 (표준오차 증가).
- 회귀계수의 통계적 유의성(t-값)이 낮아진다.
- 회귀계수의 부호가 예상과 다르게 나타나거나 해석이 어려워진다.
- 모델의 설명력(R-제곱)은 높게 나타날 수 있으나, 개별 변수의 영향력을 신뢰하기 어렵다.

### 다중공선성 진단 방법

- **상관계수 행렬**: 독립변수들 간의 상관계수가 높은지(예: 절댓값 0.7 이상) 확인한다.
- **분산팽창계수 (VIF, Variance Inflation Factor)**: 각 독립변수가 다른 독립변수들에 의해 얼마나 설명되는지를 나타내는 지표. VIFk=1/(1−Rk2) (Rk2는 k번째 독립변수를 종속변수로, 나머지 독립변수들을 독립변수로 하여 회귀분석했을 때의 결정계수).
    - 일반적으로 VIF > 5 이면 다중공선성을 의심하고, VIF > 10 이면 심각한 다중공선성이 있다고 판단한다.

### 다중공선성 해결 방법

- **변수 제거**: VIF가 높은 변수 중 이론적으로 덜 중요하거나 종속변수와의 관련성이 낮은 변수를 제거한다.
- **표본 크기 증가**: 현실적으로 어려운 경우가 많다.
- **변수 변환**: 로그 변환, 표준화, 정규화 또는 연속형 변수를 범주형으로 변환한다.
- **주성분 분석 (PCA) 활용**: 주성분을 새로운 독립변수로 사용한다 (해석의 어려움 발생 가능).
- **능형 회귀(Ridge Regression) 또는 Lasso 회귀 사용**: 다중공선성에 덜 민감한 모델을 사용한다.
- **변수 선택 알고리즘**: 단계적 선택법(Stepwise selection), 전진 선택법(Forward selection), 후진 제거법(Backward elimination)을 활용한다.

### 섀플리 밸류 (Shapley Value) 분석

게임 이론에서 비롯된 개념으로, 여러 독립변수가 함께 모델의 설명력에 기여할 때 각 변수의 순수한 기여도를 공정하게 배분하는 방법이다.
각 변수가 모델에 포함될 때와 포함되지 않을 때의 설명력 변화(한계 기여도)를 모든 가능한 변수 조합 순서에 대해 평균 내어 계산한다. 이를 통해 다중공선성이 있는 상황에서도 각 변수의 상대적 중요도를 파악하는 데 도움을 줄 수 있다.

## 데이터 마사지와 블라인드 분석

### 데이터 마사지 (Data Massage)

데이터 분석 결과가 예상하거나 의도한 방향과 다를 때, 데이터의 수치를 직접 조작하는 것이 아니라 데이터의 배열을 수정하거나 관점을 바꾸는 등의 방법으로 해석을 유도하는 행위이다. 분석가의 주관이 개입되므로 지양해야 한다.

### 편향된 데이터 전처리

이상치나 결측값을 처리할 때 분석가의 의도에 유리한 방향으로 기준을 설정하거나 처리 방법을 선택하는 것이다.

### 매직 그래프 사용

그래프의 축 범위, 레이블 간격, 비율 등을 왜곡하여 실제 수치 차이보다 크거나 작게 보이도록 유도하는 것이다.

### 분모 바꾸기 등 관점 변환

동일한 비율 차이라도 기준이 되는 분모를 어떻게 설정하느냐에 따라 받아들여지는 느낌이 달라지도록 하는 것이다.

### 의도적인 데이터 누락 및 가공

원하는 방향과 반대되는 데이터를 의도적으로 누락시키거나, 여러 데이터를 합쳐 특정 추세를 만들어내는 것이다.

### 머신러닝 모델의 파라미터 값 변경 및 연산 반복

의도한 결과가 나올 때까지 모델의 파라미터 값을 변경하며 반복적으로 연산하는 것이다.

### 심슨의 역설

전체 데이터에서는 나타나지 않거나 반대 방향의 추세가 하위 그룹에서는 나타나는 현상을 의도적으로 활용하는 것이다.

### 블라인드 분석 (Blind Analysis)

데이터 분석 과정에서 분석가의 주관적 편향(인지적 편향, 확증 편향)을 최소화하기 위한 방법이다.
독립변수나 종속변수의 실제 의미나 명칭을 가린 상태에서 분석을 수행하고, 오직 통계적 결과만을 바탕으로 의미를 해석한다. 이를 통해 기존의 가설이나 경험에 의한 선입견이 분석 과정에 개입되는 것을 방지하고자 한다.

## Z-검정과 T-검정 (Z-test and T-test)

### Z-검정과 T-검정의 개요 및 조건

한 집단 또는 두 집단 간의 평균(또는 비율) 차이가 통계적으로 유의미한지를 검정하는 방법이다.

- **기본 가정**:
    - 분석 대상 변수는 양적 변수 (평균 검정 시).
    - 데이터는 정규분포를 따른다 (Shapiro-Wilk 검정 등으로 확인).
    - (두 집단 검정 시) 등분산성: 두 집단의 분산이 동일하다 (Levene 검정, Bartlett 검정 등으로 확인). 등분산 가정이 충족되지 않으면 Welch's t-test를 사용한다.

### 검정 방법의 선택 기준

| 조건 | 검정 방법 |
| --- | --- |
| 모집단 분산(σ2)을 아는 경우 | Z-검정 |
| 모집단 분산을 모르고, 표본 크기(n) ≥ 30 | Z-검정 |
| 모집단 분산을 모르고, 표본 크기(n) < 30 | T-검정 |

실제로는 모집단 분산을 아는 경우가 드물고, 표본 크기가 커지면 t-분포가 정규분포에 근사하므로 T-검정이 더 보편적으로 사용된다.

### 가설 검정 절차

1. **가설 설정**: 귀무가설(H0: 차이가 없다)과 대립가설(H1: 차이가 있다/크다/작다)을 설정한다.
2. **유의수준(**α**) 결정**: 보통 0.05, 0.01, 0.1 등을 사용한다.
3. **검정통계량 계산**: Z-값 또는 t-값을 계산한다.
    - t=(표본평균−모평균)/(표본표준편차/표본크기) (단일 표본)
    - t=(표본평균1−표본평균2)/표준오차 (두 표본)
4. **p-value 계산 또는 임계값과 비교**:
    - p-value < α 이면 귀무가설을 기각한다.
    - 검정통계량의 절댓값이 임계값보다 크면 귀무가설을 기각한다.
5. **결론 도출**.

### 단일 표본, 두 표본(독립, 대응) 평균 검정

- **단일 표본 T-검정 (One-sample T-test)**: 하나의 표본 평균을 특정 값(모평균)과 비교한다.
- **독립 표본 T-검정 (Independent samples T-test)**: 서로 독립적인 두 집단의 평균을 비교한다.
- **대응 표본 T-검정 (Paired samples T-test)**: 동일 대상에 대한 두 가지 조건(예: 사전-사후)에서의 평균을 비교한다.

### 단일 표본, 두 표본 비율 검정

평균 검정과 유사한 원리로, 비율의 차이를 검정한다. 비율의 분산은 $p(1-p)$를 사용한다.

## 분산분석 (ANOVA: Analysis of Variance)

### ANOVA의 개념 및 목적

셋 이상의 집단 간 평균 차이가 통계적으로 유의미한지를 검정하는 방법이다. T-검정을 여러 번 반복할 경우 발생하는 1종 오류(귀무가설이 참인데 기각할 확률) 증가 문제를 해결한다. F-분포를 사용한다.

### ANOVA의 기본 가정

- 독립변수는 범주형, 종속변수는 연속형.
- 각 집단의 데이터는 정규분포를 따른다.
- 각 집단의 분산은 동일하다 (등분산성).
- 관측치는 서로 독립적이다.

### ANOVA의 종류

- **일원 분산분석 (One-way ANOVA)**: 하나의 독립변수(요인)에 따른 종속변수의 평균 차이를 검정한다.
- **이원 분산분석 (Two-way ANOVA)**: 두 개의 독립변수와 이들의 상호작용 효과를 검정한다.
- **다원 분산분석 (N-way ANOVA)**: N개의 독립변수 효과를 검정한다.

### ANOVA의 원리

전체 변동(Total Sum of Squares, SST)을 집단 간 변동(Between-group Sum of Squares, SSB)과 집단 내 변동(Within-group Sum of Squares, SSW)으로 분해한다.

- **집단 간 분산 (**MSB**)**: SSB / (집단 수 - 1)
- **집단 내 분산 (**MSW**)**: SSW / (전체 표본 수 - 집단 수)
- **F-통계량**: MSB/MSW. 집단 간 분산이 집단 내 분산에 비해 상대적으로 크면 F-값이 커지고, 이는 집단 간 평균 차이가 유의미할 가능성이 높음을 의미한다.

### 사후 검정 (Post Hoc Tests)

ANOVA 검정 결과, 집단 간 평균 차이가 유의미하다는 결론(귀무가설 기각)이 나오면, 구체적으로 어떤 집단들 간에 차이가 있는지를 파악하기 위해 사후 검정을 실시한다.

- **Tukey's HSD (Honestly Significant Difference)**: 모든 가능한 집단 쌍 간의 평균 차이를 검정한다. 집단 크기가 같을 때 주로 사용한다.
- **Scheffe's Test**: 보수적인 검정 방법으로, 집단 크기가 다르거나 복잡한 비교를 할 때 사용한다.
- **Bonferroni, Duncan 등**

## 카이제곱 검정 (교차분석, Chi-square Test)

### 카이제곱 검정의 개념 및 목적

두 개 이상의 범주형 변수들 간의 연관성(독립성)을 검정하는 방법이다. 명목척도 또는 서열척도 변수에 사용한다.

### 교차표 (Contingency Table)

두 범주형 변수의 각 범주 조합에 해당하는 빈도(관측빈도)를 표 형태로 나타낸 것이다.

### 관측빈도와 기대빈도

- **관측빈도 (Observed Frequency, O)**: 실제 데이터에서 관찰된 각 셀의 빈도.
- **기대빈도 (Expected Frequency, E)**: 두 변수가 서로 독립이라고 가정했을 때 기대되는 각 셀의 빈도.
    - 기대빈도 = (해당 행의 합계 * 해당 열의 합계) / 전체 합계

### 카이제곱 통계량

관측빈도와 기대빈도 간의 차이를 측정한다.

# 확인 문제

### **문제 1.**

> 🧚 경희는 다트비 교육 연구소의 연구원이다. 경희는 이번에 새롭게 개발한 교육 프로그램이 기존 프로그램보다 학습 성취도 향상에 효과적인지 검증하고자 100명의 학생을 무작위로 두 그룹으로 나누어 한 그룹(A)은 새로운 교육 프로그램을, 다른 그룹(B)은 기존 교육 프로그램을 수강하도록 하였다. 실험을 시작하기 전, 두 그룹(A, B)의 초기 시험 점수 평균을 비교한 결과, 유의미한 차이가 없었다. 8주 후, 학생들의 최종 시험 점수를 수집하여 두 그룹 간 평균 점수를 비교하려고 한다.
> 

> 🔍 Q1. 이 실험에서 사용할 적절한 검정 방법은 무엇인가요?
> 

```
독립 표본 t-검정
```

> 🔍 Q2. 이 실험에서 설정해야 할 귀무가설과 대립가설을 각각 작성하세요.
> 

```
귀무가설: 새로운 교육 프로그램(A)을 수강한 학생들의 평균 최종 시험 점수와 기존 교육 프로그램(B)을 수강한 학생들의 평균 최종 시험 점수 간에는 차이가 없다.
대립가설: 새로운 교육 프로그램(A)을 수강한 학생들의 평균 최종 시험 점수와 기존 교육 프로그램(B)을 수강한 학생들의 평균 최종 시험 점수 간에는 차이가 있다
```

> 🔍 Q3. 검정을 수행하기 위한 절차를 순서대로 서술하세요.
> 

```
가설 설정 - 유의수준 결정 - 검정통계량 선택 및 계산 - 통계적 검정
```

> 🔍 Q4. 이 검정을 수행할 때 가정해야 하는 통계적 조건을 설명하세요.
> 

```
독립성/정규성/등분산성
```

> 🔍 Q5. 추가적으로 최신 AI 기반 교육 프로그램(C)도 도입하여 기존 프로그램(B) 및 새로운 프로그램(A)과 비교하여 성취도 차이가 있는지 평가하고자 한다면 어떤 검정 방법을 사용해야 하나요? 단, 실험을 시작하기 전, C 그룹의 초기 점수 평균도 A, B 그룹과 유의미한 차이가 없었다고 가정한다.
> 

```
oneway ANOVA
```

> 🔍 Q6. 5번에서 답한 검정을 수행한 결과, 유의미한 차이가 나타났다면 추가적으로 어떤 검정을 수행해 볼 수 있을까요?
> 

```
여기에 답을 작성해주세요!
```

---

### **문제 2. 카이제곱 검정**

> 🧚 다음 중 어떠한 경우에 카이제곱 검정을 사용해야 하나요?
1️⃣ 제품 A, B, C의 평균 매출 차이를 비교하고자 한다.
2️⃣ 남성과 여성의 신체 건강 점수 평균 차이를 분석한다.
3️⃣ 제품 구매 여부(구매/미구매)와 고객의 연령대(10대, 20대, 30대…) 간의 연관성을 분석한다.
4️⃣ 특정 치료법이 환자의 혈압을 감소시키는 효과가 있는지 확인한다.
> 

```
3
```

### 🎉 수고하셨습니다.