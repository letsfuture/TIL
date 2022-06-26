# Forlium

## 1. 지도 만들기

```python
# folium을 이용해 지도 만들기
seoul = folium.Map(location=[37.55, 126.98], zoom_start=12)

# html로 저장하기
seoul.save('./seoul.html') 
```

<br>

## 2. 지도 스타일 적용하기

- `Stamen Terrain` : 산악 지형 등의 지형이 보다 선명하게 드러남.

- `Stamen Toner` : 흑백 스타일로 도로망을 강조해서 보여줌.

- 적용 예)

  ```python
  seoul = folium.Map(location=[37.55, 126.98], tiles='Stamen Terrain', zoom_start=12)
  ```

<br>

## 3. 지도에 마커 표시하기

- **지도에 하나의 마커 표시하기**

  ```python
  seolleung = folium.Map(location=[37.503376, 127.049776], zoom_start=15)
  
  folium.Marker(
      location=[37.503376, 127.049776],
      popup='선릉역'
      tooltip='2호선'
  ).add_to(seolleung)
  ```

- **지도에 여러 개의 마커 표시하기**

  ```python
  for name, alt, lng in zip(df.index, df.위도, df.경도):
      folium.Marker([lat, lng], popup=name).add_to(seoul_map)
  ```

  - **zip(*iterable) 함수**

    - `zip(*iterable)`은 **동일한 개수**로 이루어진 자료형을 묶어 주는 역할을 하는 함수

    - `*iterable`은 반복 가능한 자료형 여러 개를 입력할 수 있다는 의미

- **지도에 여러 개의 원형 마커 표시하기**

  ```python
  for name, lat, lng in zip(df.index, df.위도, df.경도):
      folium.CircleMarker([lat, lng],
                         radius=10,
                         color='brown',
                         fill=True,
                         fill_color='coral',
                         fill_opacity=0.7,
                         popup=name).add_to(seoul_map)
  ```

- **마우스로 클릭할 때마다 마커 생성하기**

  ```python
  # folium.ClickForMarker()
  seolleung = folium.Map(location=[37.503376, 127.049776],
                        zoom_start=15)
  seolleung.add_child(folium.ClickForMarker(popup='ClickForMarker'))
  ```

  - `popup` 에는 원하는 문구를 써주면 됨.

- **마우스로 클릭할 때마다 위도, 경도 정보 반환해주기**

  ```python
  # folium.LatLngPopup()
  seolleung = folium.Map(location=[37.503376, 127.049776],
                        zoom_start=15)
  seolleung.add_child(folium.LatLngPopup())
  ```

<br>

## 4. 지도 영역에 단계구분도(Choropleth Map) 표시하기

- **경기도 시군구 경계 정보를 가진 geo-json 파일 불러오기**

  ```python
  geo_path = '경기도행정구역경계.json'
  try:
      geo_data = json.load(open(geo_path, encoding='utf-8'))
  except:
      geo_data = json.load(open(geo_path, encoding='utf-8-sig'))
  ```

  - `try, excpet` 구문을 사용해 기본적으로 `'utf-8'`로 encoding을 시도해보고, 안 되면 `'utf-8-sig'`로 encoding을 하라는 것

- **경기도 지도 만들기**

  ```python
  g_map = folium.Map(location=[37.5502, 126.982], tiles='Stamen Terrain', zoom_start=9)
  ```

- **Choropleth 클래스로 단계구분도 표시하기**

  ```python
  # 예제1
  folium.Choropleth(geo_data=geo_data,
                   data=df[year],
                   columns=[df.index, df[year]],
                   fill_color='YlOrRd', fill_opacity=0.7, line_opacity=0.3,
                   threshold_scale=[10000, 100000, 300000, 500000, 700000],
                   key_on = 'feature.properties.name',
                   ).add_to(g_map)
  ```

  ```python
  # 예제2
  usa = folium.Map([43, -102], zoom_start=3)
   
  folium.Choropleth(
  	geo_data='us-states.json', # 경계선 좌표
      data = df,                 # Series 혹은 DataFrame이어야 함
      columns=['State', 'Unemployment'],
      key_on='feature.id', 
      fill_color='BuPu',
      fill_opacity=0.5,
      line_opacity=0.2,
      legend_name='Unemployment rate(%)').add_to(usa)
  ```

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.161-169