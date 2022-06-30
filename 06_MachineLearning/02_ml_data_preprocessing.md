# 데이터 전처리

## 1. 누락 데이터 처리

```python
from sklearn.model_selection import train_test_split # train, test 분류를 쉽게 하기 위한 모듈
from sklearn.impute import SimpleImputer             # 결측 데이터를 쉽게 대체하기 위한 모듈
```

```python
x = df.values[:, :-1] # 행은 다 가져오고, 열(컬럼)은 마지막을 제외하고 가져와라
y = df.values[:, -1]  # 행은 다 가져오고, 열(컬럼)은 마지막만 가져와라

imp_mean = SimpleImputer(strategy='mean') # NaN 값을 평균값으로 대체
imp_mean = imp_mean.fit(x[:, 1:3])
x[:, 1:3] = imp_mean.transform(x[:, 1:3])
```

- `x[:, 1:3] = imp_mean.fit_transform(x[:, 1:3])`으로 써도 됨.

<br>

## 2. feature scaling

### 1) 표준화(Standardization)

- 값의 분포를 평균이 0이고 분산이 1인 가우시안 정규분포를 가진 값으로 변환

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
x[:, 1:3] = scaler.fit_transform(x[:, 1:3])
```

### 2) 정규화(Normalizaiton)

- 데이터의 분포가 정규 분포가 아닐 경우 적용

- 0과 1사이의 값을 가짐.

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
x[:, 1:3] = scaler.fit_transform(x[:, 1:3])
```

```python
X_train, X_test, y_train, y_test = train_test_split(x, y,
                                                    test_size=0.2,
                                                    random_state=42)
```

<br>

## 3. fit(), transform(), fit_transform()의 차이

- 학습 데이터 셋으로 `fit()`된 Scaler를 이용해 테스트 데이터 셋을 변환할 경우, <u>테스트 데이터 셋에는 다시 `fit()`하지 않고 반드시 그대로 학습 데이터 셋에서 `fit()`된 Scaler를 이용</u>해 `transform()`을 수행해야 함.

  :point_right: 학습할 때와 테스트할 때  모두 <u>동일한 기반에서 데이터 변환</u>이 이루어져야 하기 때문임.

- 이때 `fit()`을 하고 `transform()`을 이용할 때, 절차를 **간소화**해 한꺼번에 사용할 수 있는 것이 `fit_transform()`임.

```python
from sklearn.datasets import load_iris
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler, StandardScaler
from sklearn.metrics import accuracy_score

iris = load_iris()
iris_data = iris.data
iris_label = iris.target

X_train, X_test, y_train, y_test = train_test_split(iris_data,
                                                    iris_label, 
                                                    test_size=0.2,
                                                    random_state=2)

scaler = MinMaxScaler()
scaler.fit(X_train)
scaled_X_train = scaler.transform(X_train)
scaled_X_test = scaler.transform(X_test)

lr = LogisticRegression()
lr.fit(scaled_X_train, y_train)
pred = lr.predict(scaled_X_test)
print('예측 정확도: {0:.4f}'.format(accuracy_score(y_test,pred)))
```

- 이때 `scaled_X_train = scaler.fit_transform(X_train)` 를 사용해 `fit()`과 `transform()` 을 한꺼번에 수행해 줄 수 있음. 

- 단, 테스트 데이터 셋에는 `fit_transform()`을 사용해서는 안됨.
- 또한, **학습 데이터와 테스트 데이터로 나누기 전에 먼저 Scaling 등의 전처리를 해주는 것이 좋음.**

```python
iris = load_iris()
iris_data = iris.data
iris_label = iris.target

scaler = MinMaxScaler()
scaler.fit(iris.data)
scaled_iris_data = scaler.transform(iris.data)

X_train, X_test, y_train, y_test = train_test_split(iris_data,
                                                    iris_label, 
                                                    test_size=0.2,
                                                    random_state=2)

lr = LogisticRegression()
lr.fit(scaled_X_train, y_train)
pred = lr.predict(scaled_X_test)
print('예측 정확도: {0:.4f}'.format(accuracy_score(y_test,pred)))
```

<br>

# [참고 자료]

- 권철민. "fit & transform 과 fit_transform의 차이가 무엇인가요?". Inflearn. 2020년 01월 04일. https://www.inflearn.com/questions/19038
