# 머신러닝 모형 최적화

## 변수 선택과 차원 축소

- 종속변수에 영향을 주는 변수들을 찾아 학습에 사용할 독립변수의 수를 줄이는 것
- 과적합과 변수들 사이의 다중공선성을 줄일 수 있음.
- 모형의 학습 시간을 줄일 수 있음.

### 1) 주성분 분석(PCA, Principal Component Analysis)

- 변수 선택 및 차원 축소 방법으로 널리 사용
- 상관관계가 있는 변수들을 선형결합(Linear combination)해서 분산이 극대화된 상관관계가 없는 새로운 변수(주성분)들로 축약하는 것
- 영상인식, 통계 데이터 분석(주성분 찾기), 데이터 압축, 노이즈 제거 등 여러 분야에 사용

```python
import seaborn as sns
from sklearn.decomposition import PCA

iris = sns.load_dataset('iris')
iris_X, iris_y = iris.iloc[:, :-1], iris.species

pca = PCA(n_components=2)
iris_pca = pca.fit_transform(iris_X)

# 각각의 주성분 벡터가 이루는 축에 투영(projection)한 결과의 분산
pca.explained_variance_

# 주성분 벡터를 의미하며, 근사 데이터를 만드는 단위기저벡터
# 즉 PCA의 기저벡터 방향을 나타냄
pca.components_

# 전체 변동에서 개별 pca component 별 차지하는 변동성 비율
pca.explained_variance_ratio_
```

### 2) 분류 모형의 feature importance

- 각 독립변수들이 종속변수에 영향을 주는 정도

```python
from sklearn.ensemble import RandomForestClassifier

rf_model = RandomFroestClassifier(n_estimators=10, random_state=10)
rf_model.fit(X_train, y_train)

features = pd.DataFrame(data=np.c[X.columns.values,
                                 rf_model.feature_importances_],
                       columns=['feature', 'importance'])

features.sort_values(by='importance', ascending=False, inplace=True)
features.rest_index(drop=True, inplace=True)
```

- **시각화**

```python
plt.figure(figsize=(12, 8))
plt.bar(features.feature, features.importance)
plt.show()
```

### 3) RFE(Recursive Feature Elimination) 방식

```python
# 5개의 특징이 남을 때까지 변수를 제거
rfe_model = RFE(RandomForestClassifier(n_estimators=10, random_state=10), n_features_to_select=5)
rfe_model.fit(train_X, train_Y)
```

### 4) 회귀 모형의 변수 선택

- 회귀 계수를 이용해 중요도가 높은 변수들부터 출력

### 5) SelectKBest

- 가장 높은 score에 따라 k개의 특징을 선택

```python
from sklearn.datasets import load_iris
from sklearn.feature_selection import SelectKBest, chi2

X, y = load_iris(return_X,y=True)
X.shape # (150, 4)

# iris 데이터에서 score에 가장 큰 영향을 주는 변수 1개 선택
X_new = SelectKBest(chi2, k=1).fit_transform(X, y)
X_new.shape # (150, 1)
```



