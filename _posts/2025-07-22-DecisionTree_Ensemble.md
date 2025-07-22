---
layout: post
title:  "결정 트리(Decision tree)와 앙상블(Ensemble)"
date:   2025-07-22 09:00:00 +0900
categories: [머신러닝, 인공지능, 데이터과학]
tags: [머신러닝기초]
---

## 결정 트리(Decision Tree)

---
## 앙상블(Ensemble)

### 배깅(Bagging, Bootstrap Aggregating)
배깅(Bagging)
부트 스트랩 샘플링(Bootstrap Sampling) : 중복을 허용해서 여러 개의 작은 데이터셋을 샘플링함.
Bagging의 기법을 활용한 대표적인 알고리즘으로는 랜덤 포레스트가 있음. 

#### 랜덤 포레스트(random forest)

많은 decision tree가 모여서 하나의 숲을 이루는 모델, 앙상블 기법 중 Bagging(Bootstrap aggregating)을 기반으로 작동

동작 방식
- 부트 스트랩 샘플링(Bootstrap Sampling) : 중복을 허용해서 여러 개의 작은 데이터셋을 샘플링함
- 하나의 트리 하나당 하나의 부트스트랩된 데이터 셋이 들어감.
- 특성 무작위 선택 : 여러가지 feature 중에 랜덤으로 랜덤의 수를 사용하고 이를 최적의 분할 기준을 찾음.

장점
- 과적합 방지효과 : 기존 트리의 과적합 단점 해결, 여러 트리로 평균 or 다수결로 모델 결정
- 예측 성능 향상
- 안정적인 모델

### 부스팅(Boosting)

모델들을 순차적으로 학습시키는 방식 - 순서가있음

배깅은 병렬적으로 학습시킴

첫 번째 모델이 잘못 예측한 결과에서 잘못 예측한 데이터에 더 많은 가중치를 부여하거나, 이전 모델의 잔차를 다음 모델이 학습하도록하여 알고리즘의 성능을 개선

부스팅의 핵심
순차적학습- 직렬적으로 학습
오류보정 - 이전 모델의 오류를 다음 모델이 학습하여 보정
편향감소 - 개별 모델의 예측이 가진 높은 변동성 상쇄 -> 전체적인 예측의 안정성향상

ex) AdaBoost(adaptive boosting) - 잘못 분류된 샘플에 가중치를 부여하여 다음 학습에 반영하는 초기 부스팅 알고리즘
Gradient Boosting machine(GBM) - 이전 모델의 예측과 실제 값의 차이를 학습하여 다음 모델을 만드는 방식
XGBoost, LightGBM, CatBoost - GBM을 개선해서 속도 성능을 향상시킴

AdaBoost : 분류 성능을 향상시키는 앙상블 학습
여러 개의 약한 학습기(약 50퍼 수준의 정답률, 대충 depth =1,Decision Stump)을 순차적으로 학습시키고 결합 - 강력한 학습기를 생성



```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import make_moons
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
from matplotlib.colors import ListedColormap

```