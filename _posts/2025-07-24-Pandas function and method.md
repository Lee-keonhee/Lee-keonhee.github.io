---
layout: post
title:  "Pandas 핵심 함수와 매서드 정리"
date:   2025-07-22 09:00:00 +0900
categories: [머신러닝, 인공지능, 데이터과학]
tags: [Python, Pandas]
---

## Pandas 자주 사용하는 함수와 매서드

최근 정보의 저장과 인터넷의 발달로 인해 매우 많은 데이터가 발생하고 있습니다. 하지만 이러한 방대한 데이터를 의미있는 정보로 가공하고 분석하는 능력이 현대사회의 필수적인 능력으로
자리잡고 있습니다.
파이썬은 이러한 데이터 분석 및 처리 작업에 있어 가장 강력하고 폭넓게 활용되는 프로그래밍 언어 중 하나이며,
많은 사람들이 데이터 조작과 분석을 위한 핵심 라이브러리인 **Pandas(판다스)**를 사용하고 있습니다.

많은 사람들이 Pandas를 사용함에도 불구하고, 새로 데이터에 대해 공부하는 사람들은 Pandas가 제공하는 기능이 워낙 다양하기 때문에, 어떤 기능을 익히고 활용해야하는지 파악하기 어렵습니다.
이번 시간에는 Pandas 라이브러리의 방대한 기능 중 실제 데이터 분석 및 전처리 과정에서 가장 빈번하게 활용되는 핵심 함수와 메서드들을 엄선하여 소개하고자 합니다.


Pandas를 사용하기 위해서 pandas 라이브러리를 불러와야 한다.
```python
import pandas as pd
```

### Pandas 모듈 함수
- pd.read_csv(경로), pd.read_excel(경로): csv 및 excel 파일을 읽어서 Dataframe 형식으로 변환 (자주 사용하는 파라미터 sep=';': 데이터 구분자가 ,가 아닌 ;일때 사용)
```python
df = pd.read_csv(
    '파일경로',
    sep=';',                        # 구분자가 세미콜론
    encoding='utf-8',               # 한글 깨짐 방지
    header=0,                       # 첫 행이 열 이름
    index_col="id",                 # 'id' 열을 인덱스로
    usecols=["id", "name", "date"], # 사용할 컬럼만 따로 dataframe 생성
    parse_dates=["date"],           # 날짜 형식으f로 파싱 - 날짜 형식을 추론해서 자동 변경
    na_values=["-", "없음"]          # 결측값 처리
)  
```

- pd.DataFrame({'컬럼1': [값1, 값2], '컬럼2': [값3, 값4]}): 직접 데이터를 넣어서 새로운 DataFrame을 생성

1. 리스트를 이용하여 데이터프레임 생성
```python
df_from_list = pd.DataFrame([[1,2],[3,4]],columns=['A','B'], index=['row1', 'row2'])
```
생성된 데이터프레임
|     | A | B |
|-----|---|---|
| 1   | 1 | 2 |
| 2   | 3 | 4 |

2. 딕셔너리를 이용한 데이터프레임 생성
```python
df_from_dict = pd.DataFrame({'이름':['홍길동', '이순신'], '나이':[25,30]})
```

생성된 데이터프레임

3. numpy 배열을 이용한 데이터프레임 생성

```python
import pandas as pd
import numpy as np

arr = np.array([[1, 2], [3, 4]])
df_from_numpy = pd.DataFrame(arr,columns=['A','B'])
```

생성된 데이터프레임


- pd.concat([df1, df2, df3]): 여러 개의 DataFrame을 위아래(행 기준)나 옆으로(열 기준) 이어붙임

- pd.merge(df1, df2, on='컬럼명'): 두 DataFrame을 특정 '키'를 기준으로 병합
- pd.get_dummies(df['컬럼명']): 범주형 데이터를 원-핫 인코딩(One-Hot Encoding)방식으로 숫자로 변경. 범주형 데이터의 종류만큼 column을 가짐
- 
