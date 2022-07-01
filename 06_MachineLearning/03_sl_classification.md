# 지도 학습(Supervised Learning)

## 분류(Classification)

### 1) KNN(K-Nearest-Neighbors)

- 새로운 관측값이 주어지면 기존 데이터 중에서 <u>가장 속성이 비슷한 k개의 이웃을 찾아, 가까운 이웃들이 갖고 있는 목표 값과 같은 값으로 분류</u>하여 예측

- k값에 따라 예측의 정확도가 달라지므로, <u>적절한 k값을 찾는 것이 매우 중요</u>

  ```python
  from sklearn import preprocessing
  from sklearn.model_selection import train_test_split
  from sklearn.neighbors import KNeighborsClassifier
  ```

  ```python
  X = preprocessing.StandardScaler().fit(X).transform(X)
  X_train, X_test, y_train, y_test = train_test_split(X,
                                                     y,
                                                     test_size=0.3,
                                                     random_state=42)
  # knn 객체 생성(k=5로 설정)
  knn = KNeighborsClassifier(n_neighbors=5)
  
  # train data를 가지고 모델 학습
  knn.fit(X_train, y_train)
  
  # test data를 통해 y_hat을 예측(분류)
  y_hat = knn.predict(X_test)
  
  # 모델 성능 평가
  knn_matrix = metrics.confusion_matrix(y_test, y_hat)                        # confusion matrix
  knn_report = metrics.classification_report(y_test, y_hat, output_dict=True) # confusion matrix를 이용해 계산한 값
  knn_report = pd.DataFrame(knn_report).transpose() 
  ```

<br>

### 2) SVM(Support Vector Machine)

- 벡터 공간에 위치한 훈련 데이터의 좌표와 각 데이터가 어떤 분류 값을 가져야 하는지 정답을 입력 받아서 학습

- 선형 또는 비선형 분류 뿐만 아니라 회귀, 이상치 탐색에서도 사용할 수 있는 모델이며, 특히 복잡한 분류 문제에 잘 맞으며, 중간 크기의 데이터셋에 적합

- 마진(margin)을 가장 크게 하는 초평면(hyperplane)의 방향, w을 찾는 것

  ```python
  from sklearn import svm
  from sklearn import metrics
  ```

  ```python
  # svm 모듈의 SVC() 함수를 사용해 svm_model 객체 생성
  svm_model = svm.SVC(kernel='rbf') # rbf: Radial Basis Function
  
  # train data를 가지고 모델 학습
  svm_model.fit(X_train, y_train)
  
  # test data를 통해 y_hat을 예측(분류)
  y_hat = svm_model.predict(X_test)
  
  # 모델 성능 평가
  svm_matrix = metrics.confusion_matrix(y_test, y_hat) 
  svm_report = metrics.classification_report(y_test, y_hat, output_dict=True) 
  svm_report = pd.DataFrame(knn_report).transpose()
  ```

- `kernel` : 데이터를 저차원(L) **고차원(H)**으로 매핑시켜, 고차원 공간에서 데이터를 분류하고자 사용
  - 선형(linear) 커널, 다항식(poly) 커널, 가우시안 커널(=rbf), 시그모이드(sigmoid) 커널  

<br>

### 3) 의사결정나무(Decision Tree)

- 트리 구조를 사용하며, 각 분기점에는 분석 대상의 속성들이 위치함.

- 각 분기점마다 목표 값을 가장 잘 분류할 수 있는 속성을 찾아서 배치하고, 해당 속성ㄱ이 갖는 값을 이용하여 새로운 가지를 만듦.

- Entropy가 일정 수준 이하로 낮아질 때까지 과정을 반복해 최적의 속성으로 분류할 수 있도록 함(<u>Entropy가 낮을수록 분류가 잘된 것임</u>).

  ```python
  from sklearn import tree
  ```

  ```python
  tree_model = tree.DecisionTreeClassifier(criterion='entropy', max_depth=5)
  tree_model.fit(X_train, y_train)
  
  y_hat = tree_model.predict(X_test), output_dict=True
  
  tree_matrix = metrics.confusion_matrix(y_test, y_hat)
  
  tree_report = metrics.classification_report(y_test, y_hat, output_dict=True)
  tree_report = pd.DataFrame(tree_report).transpose()
  ```

  - `criterion` : 분할 품질을 측정하는 기능으로 default는 `gini`임.
    - `gini`, `entropy`, `log_loss` 
  - `max_depth` : 트리의 최대 깊이(값이 클수록 모델의 복잡도가 올라감)

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.308-330
- sklearn, "sklearn.tree.DecisionTreeClassifier" https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html
- Excelsior-JH, "서포트 벡터머신, SVM - (2)", EXCELSIOR, 2018년 8월 16일, https://excelsior-cjh.tistory.com/165
