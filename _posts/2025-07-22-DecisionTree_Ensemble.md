---
layout: post
title:  "결정 트리(Decision tree)와 앙상블(Ensemble)"
date:   2025-07-22 09:00:00 +0900
categories: [머신러닝, 인공지능, 데이터과학]
tags: [머신러닝기초]
---
---
---
## 결정 트리(Decision Tree)
**결정 트리(Decision Tree)**는 의사결정트리라고도 불리며, **분류(classification)**와 회귀(regression) 문제 모두에 사용할 수 있는 지도 학습(supervised learning) 모델입니다.

결정 트리는 **특정 기준(예: 불순도 감소(분류), 분산 감소(회귀) 등)**에 따라 데이터를 분할하며, 각 분할 기준은 특성(feature) 값에 기반합니다.
데이터는 **루트 노드(root node)**에서 시작해 조건에 따라 왼쪽 또는 오른쪽 자식 노드로 나누어지며, **리프 노드(leaf node)**에 도달할 때까지 반복적으로 분할됩니다.

(여기 결정트리 그림 넣기)

---

### 문제 유형에 따른 출력 방식
- 분류 문제 (Classification)
리프 노드에 도달한 샘플들의 **최빈값(majority class)**을 대표값으로 사용해 예측합니다.

- 회귀 문제 (Regression)
리프 노드에 도달한 샘플들의 **평균값(mean)**을 대표값으로 사용해 예측합니다.

---

### 분할 기준
결정 트리는 노드 분할 시, 분할 후 발생하는 불확실성이나 오차를 최소화하는 최적의 기준을 찾습니다. 문제 유형에 따라 사용하는 기준이 달라집니다.
1. 분류문제 : 불순도(Impurity) 감소
- ***불순도(Impurity)*** : 특정 노드 안에 있는 데이터 샘플들이 얼마나 섞여 있는지, 즉 얼마나 균일하지 않은지를 나타내는 척도를 나타냅니다.
- ***지니 불순도*** : 무작위로 선택한 샘플이 잘못 분류될 확률을 측정합니다. 계산이 간단하여 많이 사용됩니다.
- ***엔트로피(Entropy)*** : 노드 내 데이터의 무질서도나 불확실성을 나타냅니다. 엔트로피가 낮을수록 순수합니다.
<br>
2. 회귀 문제: 분산 및 평균제곱오차(MSE) 최소화
- 회귀 트리에서는 노드의 예측값으로 해당 노드에 속한 샘플들의 평균을 사용합니다.
- 평균제곱오차(Mean Squared Error, MSE): 노드 내 샘플들의 실제 값과 해당 노드의 평균 예측값 사이의 오차를 측정합니다. MSE가 작다는 것은 해당 노드의 데이터가 평균 주변에 **더욱 밀집되어 있음(분산이 작음)**을 의미합니다.

---

### 장점
- 해석 용이성 (시각화 쉬움)
- 비선형 관계 포착.

### 단점 
- 과적합(Overfitting)에 취약 (-> 앙상블 활용)

```python
from sklearn.tree import DecisionTreeClassifier
tree = DecisionTreeClassifier(max_depth='트리 깊이 제한(int)',
                              min_samples_split='노드를 분할하는데 필요한 최소 샘플수(int)',
                              min_samples_leaf='리프노드의 최소 샘플 수(int)')
```

---
---

## 앙상블(Ensemble)

앙상블은 여러 개의 **약한 학습기(weak learners)**를 결합하여 **하나의 강력한 학습기(strong learner)**를 만드는 머신러닝 기법입니다. 단일 모델의 한계를 극복하고 예측 성능과 안정성을 높이는 데 효과적입니다.

---
### ***배깅(Bagging, Bootstrap Aggregating)***
- 배깅(Bagging)
부트 스트랩 샘플링(Bootstrap Sampling) : 중복을 허용해서 여러 개의 작은 데이터셋을 샘플링함
Bagging의 기법을 활용한 대표적인 알고리즘으로는 랜덤 포레스트가 있음.

#### ***랜덤 포레스트(random forest)***

많은 decision tree가 모여서 하나의 숲을 이루는 모델, 앙상블 기법 중 Bagging(Bootstrap aggregating)을 기반으로 작동

***동작 방식***
- 부트 스트랩 샘플링(Bootstrap Sampling) : 중복을 허용해서 여러 개의 작은 데이터셋을 샘플링
- 하나의 트리 하나당 하나의 부트스트랩된 데이터 셋이 들어감
- 특성 무작위 선택 : 여러가지 feature 중에 랜덤으로 랜덤의 수를 사용하고 이를 최적의 분할 기준을 찾음

***장점***
- 과적합 방지효과 : 부트 스트랩 샘플링, 특성 무작위 선택 -> 다양한 트리 생성을 통해 서로의 단점 보완
- 예측 성능 향상
- 안정적인 모델
- 특성 중요도(Feature Importance) 제공 : 어떤 특성이 모델의 예측에 가장 큰 영향을 미치는 지 알 수 있음

***단점*** 
-  개별 트리가 복잡할수록 (트리가 많아질수록) 모델의 해석이 어려워짐

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
tree = RandomForestClassifier(n_estimators='생성할 트리의 수(int)',
                              min_samples_split='노드를 분할하는데 필요한 최소 샘플수(int)',
                              min_samples_leaf='리프노드의 최소 샘플 수(int)',
                              max_depth='트리 깊이 제한(int)',
                              criterion='평가방법(gini, entropy)',
                              n_jobs=-1,
                              )
```

---

### ***부스팅(Boosting)***

부스팅은 배깅과 달리 모델들을 **순차적으로(직렬적으로)** 학습시키는 앙상블 기법입니다. 이전 모델의 예측 오차를 다음 모델이 학습하여 점진적으로 성능을 개선해나가는 방식입니다. 주로 모델의 편향(Bias)을 줄이는 데 집중하며, 이를 통해 최종 모델의 정확성을 크게 향상시킵니다.

1. 부스팅의 핵심
- 순차적학습- 직렬적으로 학습
- 오류보정 - 이전 모델의 오류를 다음 모델이 학습하여 보정
- 편향감소 - 개별 모델의 예측이 가진 높은 변동성 상쇄 -> 전체적인 예측의 안정성향상

2. 부스팅의 예시
- AdaBoost(adaptive boosting) - 잘못 분류된 샘플에 가중치를 부여하여 다음 학습에 반영하는 초기 부스팅 알고리즘
- Gradient Boosting machine(GBM) - 이전 모델의 예측과 실제 값의 차이를 학습하여 다음 모델을 만드는 방식
- XGBoost, LightGBM, CatBoost - GBM을 개선해서 속도 성능을 향상시킴


AdaBoost : 분류 성능을 향상시키는 앙상블 학습
여러 개의 약한 학습기(약 50퍼 수준의 정답률, 대충 depth =1,Decision Stump)을 순차적으로 학습시키고 결합 - 강력한 학습기를 생성
스텀프의 성능 : 1/2 log ((1- total_error)/total_error)
error가 작으면 성능이 급격히 늘어나고, error가  크면 성능이 급격히 줄어든다.
cost 함수 L(y, f(x)) = e^-(y*f(x))
y : 실제 클래스 레이블 (ex -1, 1)
f(x) : 약한 학습기의 예측값 or 최족 분류기의 예측 점수
맞추면, cost가 줄어들고, 예측값과 다르면 cost가 커짐.


- Gradient Boosting Machine(GBM)
이전 잔차의를 다음 약한 학습기가 학습 - 전체 모델을 개선해나감

- XGBoost
경사하강법 기반- 그래디언트 부스팅을 효율, 유연, 성능 측면의 극대화 - 빠른 학습속도와 높은 예측 정확도

---
### ***스태킹(Stacking)***

---

[결정트리와 랜덤 포레스트 구현 코드 확인하기]({{site.baseurl}}/2025/07/DecisionTree_RandomForest_code/)
---