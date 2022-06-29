# 머신러닝 기초

## 머신러닝의 종류

### 1. 지도 학습(Supervised Learning) ###
- 목표 변수가 있음.

1. **분류(Classification) :point_right:** y가 이산값
   - KNN(K-nearest neighbors)
   - Naive Bayes
   - Logistic Regression
   - Random Forest
   - Support Vector Machine
   - ANN(Articifial Neural Network)
2. **추정(Estimation)** :point_right: y가 연속값
   - Linear Regressior(Stepwise)
   - Regularized Linear Regression
   - Regression Tree
   - Random Forest Regression
   - Support Vector Regression

<br>

### 2. 비지도 학습(Unsupervised Learning) ###

- 목표 변수가 없음.

1. **차원 축소(Dimension Reduction)**
   - PCA(Principal Component Analysis)
   - Factor Analysis
   - MDS(Multi-Dimensional Scaling)

2. **군집화(Clustering)**
   - Hierarchical Clustering
   - K-means Clustering, Kmedio
   - SOM(Self-Organizing Map)

3. **연관성 규칙 발견(Association Rule)**
   - MBA(Market Basket Analysis)
   - Sequence Analysis
   - Collaborative Filtering

<br>

### 3. 강화 학습(Reinforcement learning)

- 주어진 문제의 답이 명확히 떨어지지 않지만, 알고리즘이 수행한 결과에 따라서 보상과 손실이 주어져, 이를 통해 보상을 최대화하는 방향으로 진행하는 학습 방법.

<br>

## 사이킷런(SciKit-learn)

### 1. Estimator

1. **Classifier**
   - DecisionTreeClassifier
   - RandomForestClassifier
   - GradientBoostingClassifier
   - GaussianNB
   - SVC
2. **Regressor**
   - LinearRegression
   - Ridge
   - Lasso
   - RandomForestRegressor
   - GradientBoostingRegressor

<br>

### 2. 사이킷런 주요 모듈

  - **데이터 분리, 검증, 파라미터 튜닝**

    - `sklearn.model_selection`
  - **피처 처리**

    - `sklearn.preprocessing`
    - `sklearn.feature_selection`
    - `sklearn.feature_extraction`
  - **피처 처리 및 차원 축소**

    - `sklearn.decomposition`
  - **머신러닝 알고리즘**

    - `sklearn.ensemble`
    - `sklearn.linear_model`
    - `sklearn.naiv_bayes`
    - `sklearn.neigbors`
    - `sklearn.svm`
    - `sklearn.tree`
  - **평가**

    - `sklearn.metrics`
  - **유틸리티**

    - `sklearn.pipeline`

<br>

### 3. 홀드 아웃(Hold-out)

- 데이터를 훈련 데이터와 테스트 데이터 분리

  - `train_test_split(`)

  ```python
  from sklearn.model_selection import train_test_split
  
  X_train, X_test, y_train, y_test = train_test_split(iris_data.data,
                                                     iris_data.target,
                                                     test_size=0.3,
                                                     random_state=0)
  ```

  - `shuffle` : 데이터를 분리하기 전에 데이터를 미리 섞을지를 결정, default는 True.
  - `random_state `: 호출할 때마다 동일한 학습/테스트용 데이터 세트를 생성하기 위해 주어지는 난수 값으로, <u>재현율을 보장받기 위해서는 옵션을 설정해야 함.</u>

<br>

### 4. 교차 검증

1. **K-Fold Cross Validation**
   - K개의 Fold 셋을 만들어 K번 만큼 각 Fold 셋에 학습과 검증 평가를 반복적으루 수행하는 방법
   - <u>데이터의 개수가 적은 데이터 셋에 대하여 정확도를 향상</u>시킬 수 있음.
2. **Stratified K-Fold Cross Validation**

   - 불균형 분포도를 가진 레이블(결정 클래스) 데이터 집합을 위한 K-Fold 방식
3. **Cross_val_score**

   - Fold set을 추출하고, 학습, 예측, 평가를 한 번에 수행할 수 있음.


- **사이킷런의 KFold를 이용한 교차 검증 방법**

  ```python
  from sklearn.model_selection import KFold
  
  cv = KFold(n_splits=5, shuffle=True, random_state=0)
  for train_index, test_index in cv.split(x):
      print('train_index\n', train_index)
      print('.'*70)
      print('test_index\n', test_index)
      print('='*70)
  ```

<br>

## 데이터 분석의 실수

1) **과대적합(Overfitting)**

   - 모델이 training data set에서는 좋은 성능을 내지만 validation data set에서는 낮은 성능을 내는 경우
   - **과대적합 해결 방법**
     1. 훈련 데이터를 더 많이 모으기
     2. 정규화(Regularization)
        - 규제, 드롭-아웃  등 다양한 방법을 이용해 적당한 복잡도를 가지는 모델을 자동적으로 찾아주는 기법
     3. 훈련 데이터의 잡음을 줄이기(오류 수정과 이상치 제거)
   - **[참고] 하이퍼파라미터**
     - 규제 :point_right: 모델을 단순하게 하고 과대적합의 위험을 감소시키기 위해 모델에 제약을 가하는 것
     - 하이퍼파라미터 :point_right: 학습하는 동안 적용할 규제의 양
     - 하이퍼파라미터는 학습 알고리즘으로부터 영향을 받지 않으며, 훈련 전에 미리 지정되어 훈련하는 동안에는 상수로 남아 있게 됨.
2) **과소적합(Underfitting)**

   - training data set과 validation data set의 성능에는 큰 차이가 없지만 모두 낮은 성능을 내는 경우

   - **과소적합 해결 방법**
     1. 파라미터가 더 많은 복잡한 모델을 선택
     2. 모델의 제약을 줄이기(규제 하이퍼 파라미터 값 줄이기)
     3. 조기종료 시점(overfitting이 되기 전의 시점)까지 충분히 학습

# [참고 자료]

- 예비개발자. "머신러닝 - 과대적합(overfitting)과 과소적합(underfitting), 정규화". 개발자의 개발 정보와 리뷰(블로그). 2018년 07월 22일. https://m.blog.naver.com/qbxlvnf11/221324122821

