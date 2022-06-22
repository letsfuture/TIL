# Matplotlib

## 1. 선 그래프

- **선 그래프 그리기**

  ```python
  seoul = df.loc['서울특별시']
  plt.plot(seoul.index, seoul.values, marker='o', markersize=10) # seoul.index = x축, seoul.values = y
  ```

<br>

## 2. 면적 그래프(area plot)

- **면적 그래프 그리기**

  ```python
  df.plot(kind='area', stacked=False, alpha=0.2, figsize=(20, 10))
  ```

  - `stacked = Flase` 옵션을 지정하면 각 열의 선 그래프들이 누적되지 않고 서로 겹치도록 표시됨.

  - `stacked = True` 옵션을 지정하면 선 그래프들이 서로 겹치지 않고 위아래로 데이터가 누적되게 표시할 수 있음.

<br>

## 3. 막대 그래프(bar plot)

-  시계열 데이터를 표현하는데 적합

- **막대 그래프 그리기**

  ```python
  df.plot(kind='bar', figsize=(20, 10), width=0.7, color=['orange', 'green', 'skyblue', 'blue'])
  ```

  - 가로형 막대 그래프는 `kind='barh'`

<br>

## 4. 히스토그램(histogram)

- **히스토그램 그리기**

  ```python
  df.plot(kind='hist', bins=10, color='coral', figsize=(10, 5))
  ```

<br>

## 5. 산점도(scatter plot)

- **산점도 그리기**

  ```python
  df.plot(kind='scatter', x='weight', y='mpg', c='coral', s=10, figsize=(10, 5))
  # c: 점의 색상, s: 크기
  ```

- **버블 차트 그리기** 

  - 버블 차트: 값의 크기에 따라 점의 크기를 값에 따라 다르게 표시

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

  - `vert=False` 옵션을 적용하면 수평으로 나옴.

<br>

## 8. 기타

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

- **`shift()` 메소드**

  - `df['전날거래량'] = df['거래량'].shift(1)`
  - 이때 `df['증감률']`을 만든다고 하면, 계산식은 `((df['거래량']/df['전날거래량'])-1)*100`이 됨. 이는 `(df['거래량'] - df['전날거래량'])/df['전날거래량']`과 같음.

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.108-146.
- 조대표 외 1명, 『금융 데이터 분석을 위한 파이썬 판다스』, 위키독스, 06장 시계열 데이터 03) 컬럼 시프트.
