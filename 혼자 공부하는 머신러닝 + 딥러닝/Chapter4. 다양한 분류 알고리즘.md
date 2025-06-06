# Chapter 4. 다양한 분류 알고리즘

## 4-1. 로지스틱 회귀

### 1) 럭키백의 확률

- **럭키백(Lucky Bag)**: 구성품을 확인하지 않고 먼저 구매한 뒤 나중에 알게 되는 형태
- 예시: 생선 7개의 **길이, 높이, 두께, 대각선 길이, 무게** 등의 특성(feature)을 기반으로 **생선 종류를 예측**
- 출력은 **확률**이지만, 최종적으로 **분류(classification)**가 목표이므로 **분류 문제**
- 확률은 **회귀처럼 연속값을 출력**하므로 혼동될 수 있음 → 하지만 **0 또는 1로 분류해야** 하므로 분류 알고리즘에 해당

### 2) 데이터 준비하기

- `pandas.read_csv()` 함수를 이용해 인터넷에서 직접 CSV 파일을 다운로드
- **CSV (Comma Separated Values)**: 쉼표로 구분된 텍스트 형식 데이터
- CSV 파일을 **데이터프레임(DataFrame)** 형태로 변환하여 활용

### 3) 로지스틱 회귀(Logistic Regression)

- 이름은 회귀(Regression)이지만, 실제로는 **이진 분류 모델**
- 선형 회귀처럼 **선형 방정식**을 기반으로 함

  $$
  z = a \cdot \text{무게} + b \cdot \text{길이} + c \cdot \text{대각선} + d \cdot \text{높이} + e \cdot \text{두께} + f
  $$

- 가중치 또는 계수: $a$, $b$, $c$, $d$, $e$
- $z$는 실수이므로 **0~1 사이 확률 값**으로 변환해야 함 → **시그모이드 함수** 사용

  $$
  \sigma(z) = \frac{1}{1 + e^{-z}}
  $$

- 결과 해석:
  - 예측 확률이 **0.5 이상**이면 양성(positive)
  - **0.5 미만**이면 음성(negative)으로 분류

---

## 4-2. 확률적 경사 하강법 (SGD: Stochastic Gradient Descent)

### 1) 점진적인 학습

- **온라인 학습** 또는 **스트리밍 데이터**처럼 **데이터가 점진적으로 들어오는 상황**에 적합
- 전체 데이터가 준비되지 않았거나 메모리에 모두 담기 힘들 때 활용
- **경사 하강법(Gradient Descent)**의 변형 중 하나

#### 경사 하강법 종류 비교

| 방법               | 특징                                         |
|------------------|--------------------------------------------|
| 배치(Batch)      | 전체 훈련 데이터를 사용하여 한 번에 경사 계산       |
| 확률적(SGD)       | 훈련 세트에서 **무작위로 하나**의 샘플을 선택해 경사 계산 |
| 미니배치(Mini-batch) | 소규모 샘플 묶음을 사용하여 경사 계산                 |

- **에포크(Epoch)**: 훈련 세트를 한 번 모두 사용하는 과정

### 2) 손실 함수 (Loss Function)

- 모델이 얼마나 잘못 예측했는지를 **수치로 표현**
- 손실 함수는 **연속적이고 미분 가능**해야 함 (경사 하강법 적용을 위해)
- 전체 데이터의 손실 함수의 합 = **비용 함수(Cost Function)**  
  → 둘을 엄밀히 구분하진 않지만 의미상은 다름

#### 대표적인 손실 함수 예시

- **이진 분류**: 로그 손실 함수 (Log Loss 또는 Binary Cross Entropy)

  $$
  \text{Loss} = -\left[ y \log(\hat{y}) + (1 - y)\log(1 - \hat{y}) \right]
  $$

- **회귀 문제**: 평균 제곱 오차 (MSE)

  $$
  \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
  $$

---

## ✅ 요약

- 로지스틱 회귀는 회귀처럼 보이지만 **이진 분류 문제**에 활용됨
- 선형 방정식 + 시그모이드 함수로 **확률 예측 후 분류**
- 확률적 경사 하강법은 **메모리 효율적**, **스트리밍 학습에 적합**
- 손실 함수는 **모델 성능을 정량적으로 평가**하는 핵심 도구이며, 학습에 직접 사용됨
