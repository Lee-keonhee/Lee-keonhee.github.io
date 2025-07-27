---
layout: post
title:  "결정 트리(Decision tree)와 랜덤 포레스트 코드 구현"
date:   2025-07-22 09:00:00 +0900
categories: [머신러닝, 인공지능, 데이터과학]
tags: [머신러닝기초]
---

## 결정 트리(Decision Tree)

```python
from sklearn.tree import DecisionTreeClassifier
tree = DecisionTreeClassifier(max_depth='트리 깊이 제한(int)',
                              min_samples_split='노드를 분할하는데 필요한 최소 샘플수(int)',
                              min_samples_leaf='리프노드의 최소 샘플 수(int)')
```

---

## 랜덤 포레스트(random forest)


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