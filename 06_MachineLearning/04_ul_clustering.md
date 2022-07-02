# 비지도 학습(Unsupervised Learning)

## 군집(Clustering)

- 데이터셋의 관측값이 갖고 있는 여러 속성을 분석하여 서로 비슷한 특징을 갖는 관측값끼리 같은 클러스터(집단)로 묶는 알고리즘
- 신용카드 부정 사용 방지, 구매 패턴 분석 등 소비자 행동 특성을 그룹화하는 데 사용됨.

### 1. K-Means

- 데이터 간의 유사성을 측정하는 기준으로 각 클러스터의 중심까지의 거리를 이용
- 벡터 공간에 위치한 어떤 데이터에 대하여 k개의 클러스터가 주어졌을 때 클러스터의 중심까지 거리가 가장 가까운 클러스터로 해당 데이터를 할당
- **거리 기반 알고리즘**이므로 속성의 개수가 지나치게 많을 경우 군집화의 정확도가 떨어짐.
- **최적의 K를 설정하는 방법**
  - **Elbow method:** 군집간 분산과 전체 분산의 비율을 고려하는 것
  - **Sillhouette method:** 객체와 그 객체가 속한 군집의 데이터들과의 비유사성을 계산하는 방법

```python
from sklearn import preprocessing
from sklearn import cluster
```

```python
# 정규화
X = preprocessing.StandardScaler().fit(X).transform(X)

# 모델 객체 생성
kmeans = cluster.KMeans(init='k-means++', n_clusters=5, n_init=10)

# 모델 학습
kmeans.fit(X)

# 군집화
cluster_label = kmeans.labels_
df['Cluster'] = cluster_label
```

```python
# 시각화
df.plot(kind='scatter', x='Grocery', y='Frozen', c='Cluster', cmap='Set1',
       colorbar=False, figsize=(10, 10))
df.plot(kind='scatter', x='Milk', y='Frozen', c='Cluster', cmap='Set1',
       colorbar=True, figsize=(10, 10))
```

```python
kmeans.cluster_centers # 각 군집 중심점 좌표
kmeans.n_iter          # 수행된 이동 횟수
```

  - `n_clusters` : 군집화할 수(=군집 중심점의 개수)
  - `init` : 초기 군집 중심점의 좌표 설정 방식
  - 보통은 임의로 설정하지 않고 `k-means++` 방식으로 최초 설정함.
  - `n_init` : 서로 다른 군집 중심점을 최초 셋팅
  - `max_iter` : 최대 반복 횟수

<br>

### 2. DBSCAN(Density-Based Spatial Clustering of Application with Noise)

- 데이터가 위치하고 있는 **공간 밀집도**를 기준으로 클러스터를 구분
- 자기를 중심으로 반지름 R의 공간에 최소 M개의 포인트가 존재하는 점을 **코어 포인트(core point)**라고 부름. 
- 코어 포인트는 아니지만 반지름 R 안에 다른 코어 포인트가 있을 경우 **경계 포인트(border point)**라고 함.
- 코어 포인트도 아니고 경계 포인트에도 속하지 않는 점을 **Noise(또는 outlier)**라고 분류함.
- 군집 수를 미리 정할 필요가 없으며, 불특정한 분포의 군집도 잘 찾아내며, 노이즈에 강하다는 것이 장점임.

```python
from sklearn import preprocessing
from sklearn import cluster
```

```python
# 데이터 전처리
le = preprocessing.LabelEncoder()  # label encoder 생성

le_location = le.fit_transform(df['지역']) 
le_code = le.fit_transform(df['코드']) 
le_type = le.fit_transform(df['유형']) 
le_day = le.fit_transform(df['주야']) 

df['location'] = le_location
df['code'] = le_code
df['type'] = le_type
df['day'] = le_day
```

```python
# 분석에 사용할 속성 선택
columns_list = [9, 10, 13] 
X = df.iloc[:, columns_list]

# 정규화
X = preprocessing.StandardScaler().fit(X).transform(X)

# 모델 객체 생성
dbm = cluster.DBSCAN(eps=0.2, min_samples=5)

# 모델 학습
dbm.fit(X)

# 군집화
cluster_label = dbm.labels_
df['Cluster'] = cluster_label
```

```python
# 클러스터 값으로 그룹화하고 그룹별로 내용 출력
grouped_cols = [0, 1, 3] + columns_list
grouped = df.groupby('Cluster')
for key, group in grouped:
    print('* key:', key)
    print('* number', len(group))
    print(group.iloc[:, grouped_cols].head())
    print('\n')
```

- `eps` : 이웃 반경을 뜻하는 것으로, 최대 탐색 거리를 의미하는 epsilon 값
  - 너무 작으면 모든 데이터가 군집화되지 않은 채로 남겨지게 되고, 너무 크면 데이터가 비슷하거나 하나의 군집이 되어 군집화의 의미가 없어짐.
- `min_samples` : 클러스터로 구성되기 위한 최소 샘플 개수
  - 2차원 데이터에서는 4개로 하는 것을 권장하며, 2차원보다 많은 변수를 가지고 있는 데이터셋의 경우에는 2 * dim을 추천하기도 함.
  - 데이터셋별로 데이터의 구조나 객체의 개수 n이 서로 다를 수 있으므로 데이터셋별 객체 개수 n의 특성을 감안해 결정할 수도 있음.

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.331-358
