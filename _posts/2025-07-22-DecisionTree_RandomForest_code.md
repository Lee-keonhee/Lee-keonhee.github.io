---
layout: post
title:  "결정 트리(Decision tree)와 랜덤 포레스트 코드 구현"
date:   2025-07-22 09:00:00 +0900
categories: [머신러닝, 인공지능, 데이터과학]
tags: [머신러닝기초]
---

## 결정 트리(Decision Tree)

---

## 랜덤 포레스트(random forest)


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