# 지도 학습(Supervised Learning)

## 회귀분석(Regression)

- **분석 및 학습 절차** 
  - 데이터 준비 :point_right: 데이터 탐색(`info()`, `describe()`, `unique()` 등) :point_right: 변수 선택(독립변수, 종속변수)  :point_right: 훈련/테스트 데이터 분할 :point_right: 모델 학습 및 검증

### 1) 단순회귀분석(Simple Linear Regression)
$$
Y = aX+b
$$
- 두 변수 사이에 일대일로 대응되는 확률적, 통계적 상관성을 찾는 알고리즘

- 두 변수 간의 관계를 <u>직선 형태</u>로 설명하는 알고리즘

- **변수 선택**

  - 기본적인 모듈 및 path 설정은 편의상 생략하여 적음.

  ```python
  from sklearn.model_selection import train_test_split # train data와 test data를 쉽게 나누기 위한 모듈
  from sklearn.linear_model import LinearRegression    # sklearn 라이브러리의 선형회귀분석 모듈 
  ```

  ```PYTHON
  df = [['mpg', 'cylinders', 'horsepower', 'weight']]
  
  sns.pairplot(df)
  plt.show()
  ```

  - `pairplot()`을 통해 종속변수와 선형 관계를 이루는 독립변수 찾아 변수를 선택할 수 있음.

- **훈련/테스트 데이터 분할**

  ```python
  X = df[['weight']]
  y = df['mpg']
  X_train, X_test, y_train, y_test = train_test_split(X,
                                                     y,
                                                     test_size=0.3,
                                                     random_state=42)
  ```
  
- **모델 학습 및 검증**
  
  ```python
  # 단순회귀분석 모형 객체 생성
  lr = LinearRegression()
  lr.fit(X_train, y_train)
  r_square = lr.score(X_test, y_test) # test data의 결정계수(R^2)
  a = lr.coef_                        # 회귀식의 기울기
  b = lr.intercept_                   # 회귀식의 y절편
  
  # 전체 X 데이터를 입력하여 예측한 값 y_hat을 실제 값 y와 비교
  y_hat = lr.predict(X)
  
  plt.figure(figsize=(10, 5))
  ax1 = sns.kdeplot(y, label='y')
  ax2 = sns.kdeplot(y_hat, label='y_hat', ax=ax1) # 한 그래프에 같이 표현하기 위함
  plt.legend()
  plt.show()
  ```
  

<br>

### 2) 다항회귀분석(Polynomial Regression)

$$
Y = aX^2 + bX + c
$$

- 직선보다는 곡선으로 설명하는 것이 적합할 때 사용

- 복잡한 곡선 형태의 회귀선을 표현할 수 있음

- 2차 함수 이상의 다항 함수를 이용하여 두 변수 간의 선형 관계를 설명하는 알고리즘

  ```python
  from sklearn.preprocessing import PolynomialFeatures # 다항식 변환을 위한 모듈
  ```

  ```python
  # 다항식 변환
  poly = PolynomialFeatures(degree=2)
  X_train_poly = poly.fit_transform(X_train) # 2차항으로 변형
  
  plr = LinearRegression()
  plr.fit(X_train_poly, y_train)
  
  X_test_poly = poly.fit_transform(X_test)  # test data 또한 2차항으로 변형을 위해서 fit_transform()을 사용
  plr_r_square = plr.score(X_test_poly, y_test)
  
  # 전체 X 데이터를 입력하여 예측한 값 y_hat을 실제 값 y와 비교
  X_poly = poly.fit_transform(X)
  y_hat = plr.predict(X_poly)
  ```

  - 단순회귀분석처럼 X, y 변수를 선언해주면 slice 오류가 나므로 아래와 같이 설정한 뒤, 다시 `train_test_split()` 을 이용해 데이터를 나누어야 함.

    ```python
    X = df[['weight']].values  # 독립 변수 X
    y = df['mpg'].values       # 종속 변수 Y
    ```

<br>

### 3) 다중회귀분석(Multivariate Regression)

$$
Y = b + a_{1}X_{1}+a_{2}X_{2}+…+a_{n}X_{n}
$$

- 여러 개의 독립변수가 종속변수에 영향을 주고 선형 관계를 갖는 경우 사용
- 단순회귀분석의 예제에서 독립변수의 수만 늘리면 되며, `lr.coef_` 를 사용할 경우, <u>독립변수의 개수만큼 회귀계수(회귀식의 기울기)가</u>가 리스트로 나옴.

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.286-307





