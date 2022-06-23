# Matplotlib

## 1. 선 그래프(line plot)

- 시계열 데이터와 같이 연속적인 값의 변화와 패턴을 파악하는데 적합

- 시리즈 또는 데이터프레임 객체를 plot() 함수에 직접 입력하는 것도 가능

  ```python
  seoul = df.loc['서울특별시']
  plt.plot(seoul)
  ```

- **선 그래프 그리기**

  ```python
  seoul = df.loc['서울특별시']
  plt.plot(seoul.index, seoul.values, marker='o', markersize=10) # seoul.index = x축, seoul.values = y
  ```

<br>

## 2. 면적 그래프(area plot)

- 각 열의 패턴과 함께 열 전체의 합계가 어떻게 변하는지 파악할 수 있음.

- **면적 그래프 그리기**

  ```python
  df.plot(kind='area', stacked=False, alpha=0.2, figsize=(20, 10))
  ```

  - `stacked = Flase` 옵션을 지정하면 각 열의 선 그래프들이 **누적되지 않고** 서로 겹치도록 표시됨.

  - `stacked = True` 옵션을 지정하면 선 그래프들이 서로 겹치지 않고 위아래로 데이터가 **누적되게** 표시할 수 있음.

<br>

## 3. 막대 그래프(bar plot)

-  시계열 데이터를 표현하는데 적합

- **막대 그래프 그리기**

  ```python
  df.plot(kind='bar', figsize=(20, 10), width=0.7, color=['orange', 'green', 'skyblue', 'blue'])
  ```

  - 가로형 막대 그래프는 `kind='barh'`
  
- **2축 그래프 그리기**

  ```python
  ax1 = df[['수력', '화력']].plot(kind='bar', figsize=(20, 10), width=0.7, stacked=True)
  ax2 = ax1.twinx()
  a2.plot(df.index, df.증감률, ls='--', marker='o', markersize=20, color='red', label='전년대비 증감률(%)'
  ```

<br>

## 4. 히스토그램(histogram)

- **히스토그램 그리기**

  ```python
  df.plot(kind='hist', bins=10, color='coral', figsize=(10, 5))
  ```

<br>

## 5. 산점도(scatter plot)

- 서로 다른 두 변수 사이의 관계를 나타내는 것으로, 이때 각 변수는 연속되는 값을 가짐.

- **산점도 그리기**

  ```python
  df.plot(kind='scatter', x='weight', y='mpg', c='coral', s=10, figsize=(10, 5))
  # c: 점의 색상, s: 크기
  ```

- **버블 차트 그리기** 

  - **버블 차트:** 값의 크기에 따라 점의 크기를 값에 따라 다르게 표시

  ```python
  # cylinders 개수의 상대적 비율을 계산하여 시리즈 생성
  cylinders_size = df.cylinders / df.cyliners.max() * 300 # 300을 곱해준 것은 값이 너무 작아 점이 작게 보이기 때문에 크게 하기 위함임.
  
  # 3개의 변수로 산점도 그리기
  df.plot(kind='scatter', x='weight', y='mpg', c='coral', figsize=(10, 5),
                   s=cylinders_size, alpha=0.3)
  ```

<br>

## 6. 파이 차트(pie chart)

- 파이 차트 그리기

  ```python
  # 열에 대한 파이 차트 그리기 - count 열 데이터 사용
  df_origin['count'].plot(kind='pie',
                          figsize=(7, 5),
                          autopct='%1.1f%%',
                          startangle=90, # 90으로 두지 않으면 가로로 나눠서 시작함 
                          colors=['chocolate', 'bisque', 'cadetblue']
                          )
  ```

<br>

## 7. 박스 플롯(boxplot)

- 범주형 데이터의 분포를 파악하는데 적합

- 5개의 지표(최솟값, 1분위값, 중간값, 3분위값, 최댓값)을 제공함.

  ```python
  # 그래프 객체 생성(figure에 2개의 서브 플롯 생성)
  fig = plt.figure(figsize=(15, 5))
  ax1 = fig.add_subplot(1, 2, 1)
  ax2 = fig.add_subplot(1, 2, 2)
  
  # axe 객체에 boxplot 메소드로 그래프 출력
  ax1.boxplot(x=[df[df['origin']==1]['mpg'],
                 df[df['origin']==2]['mpg'],
                 df[df['origin']==3]['mpg']],
             labels=['USA', 'EU', 'KOREA'])
  
  ax2.boxplot(x=[df[df['origin']==1]['mpg'],
                 df[df['origin']==2]['mpg'],
                 df[df['origin']==3]['mpg']],
             labels=['USA', 'EU', 'KOREA'],
             vert=False)
  ```

  - `vert=False` 옵션을 적용하면 **수평**으로 나옴.

<br>

## 8. 주석 표시(annotate)

```python
# y축 범위 지정(최솟값, 최댓값)
plt.ylim(50000, 800000)

# 주석 표시 - 화살표
plt.annotate('',
            xy=(20, 620000),    # 화살표의 머리 부분(끝점)
            xytext=(2, 290000), # 화살표의 꼬리 부분(시작점)
            xycoords='data',    # 좌표체계
            arrowprops=dict(arrowstyle='->', color='skyblue', lw=5), # 화살표 서식
            ) 

# 주석 표시 - 텍스트
plt.annotate('인구 이동 증가(1970-1995)',    # 텍스트 입력
            xy=(10, 350000),               # 텍스트 위치 기준점
            rotation=25,                   # 텍스트 회전 각도
            va='baseline',                 # 텍스트 상하 정렬
            ha='center',                   # 텍스트 좌우 정렬
            fontsize=15,                   # 텍스트 크기
            )
```

<br>

## 9. 화면 분할(axe 객체 활용)

```python
seoul = df.loc['서울특별시']

fig = plt.figure(figsize=(10, 10))
ax1 = fig.add_subplot(2, 1, 1) 
ax2 = fig.add_subplot(2, 1, 2)

ax1.plot(seoul, 'o', markersize=10)
ax2.plot(seoul, 'o', markerfacecolor='red', markersize=10,
        color='olive', lw=2, label='서울 -> 경기') # markerfacecolor는 마커 배경색을, color는 선의 색을 뜻함

# y축 범위 지정(최솟값, 최댓값)
ax1.set_ylim(50000, 800000)
ax2.set_ylim(50000, 800000)

# 축 눈금 라벨 지정 및 90도 회전
ax1.set_xticklabels(seoul.index, rotation=90)
ax2.set_xticklabels(seoul.index, rotation=90)
```

- `figure()` 함수를 사용해 그래프를 그리는 그림틀을 만든 뒤, `fig` 객체에 `add_subplot()` 메소드를 적용해 그림틀을 여러 개로 분할
- `add_subplot(행의 크기, 열의 크기, 서브플롯 순서)`
- `set_title()` : 제목 추가
- `set_xlabel()` : x축 이름 지정
- `set_ylabel()` : y축 이름 지정
- `tick_params()` : 축 눈금 라벨 크기 조절
  - 예) `ax.tick_params(axis='x', labelsize=10)`

<br>

## 10. 기타

- `plt.axis('equal')`
  - (단위가 틀리면 타원형으로도 나올 수 있으므로) 파이 차트의 비율을 원에 가깝게 조정해 주는 것

- `df.fillna(method='ffill')`을 사용하면 누락값(NaN)을 앞 데이터로 채울 수 있음.

- `rotation = 'vertical'` 옵션을 사용하면 글씨가 반시계 방향으로 90도 회전됨.
  - `rotation = 90`으로 써도 똑같음.

- **`shift()` 메소드**
  
  - `df['전날거래량'] = df['거래량'].shift(1)`
  - 이때 `df['증감률']`을 만든다고 하면, 계산식은 `((df['거래량']/df['전날거래량'])-1)*100`이 됨. 이는 `(df['거래량'] - df['전날거래량'])/df['전날거래량']`과 같음.
  
- **한글 폰트 오류 문제 해결**

  ```python
  from amtplotlib import font_manager, rc
  font_path = './Malgun Gothic.ttf'
  font_name = font_manager.FontProperties(fname=font_path).get_name()
  rc('font', family=font_name)
  ```

- **마이너스 부호 출력 설정**

  ```python
  plt.rcParams['axes.unicode_minus']=False
  ```

- **스타일 서식 시정**

  ```python
  plt.style.use('ggplot')
  ```

  - **스타일 리스트**

    ```python
    import matplotlib.pyplot as plt
    
    # 스타일 리스트 출력
    print(plt.style.available)
    ```

    ```
    ['Solarize_Light2', '_classic_test_patch', '_mpl-gallery', '_mpl-gallery-nogrid', 'bmh', 'classic', 'dark_background', 'fast', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark', 'seaborn-dark-palette', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'tableau-colorblind10']
    ```

- **그래프를 그림 파일로 저장**

  ```python
  plt.savefig('./scatter.png')
  plt.savefig('./scatter.transparent.png', transparent=True)
  ```

  - `transparent=True` 옵션은 배경을 투명하게 설정해줌.

- **컬러맵(cmap)**

  [컬러맵 참조 사이트](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.108-146.
- 조대표 외 1명, 『금융 데이터 분석을 위한 파이썬 판다스』, 위키독스, 06장 시계열 데이터 03) 컬럼 시프트.
