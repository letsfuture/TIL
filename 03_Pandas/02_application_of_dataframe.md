# 데이터프레임의 다양한 응용

## 1. 함수 매핑

### 1) 개별 원소에 함수 매핑

- **함수 매핑**: 시리즈 또는 데이터프레임의 개별 원소를 특정 함수에 일대일 대응시키는 과정

- **시리즈 원소에 함수 매핑**

  - `Seires객체.apply(매핑 함수)` : 시리즈 객체에 apply() 메소드를 적용하면 인자로 전달하는 매핑 함수에 시리즈의 모든 원소를 하나씩 입력하고 함수의 리턴값을 돌려 받음.

    ```python
    def add_10(n):
        return n + 10
    
    sr1 = df['age'].apply(add_10)
    sr2 = df['age'].apply(lambda x: add_10(x))

- **데이터프레임 원소에 함수 매핑**

  - `DataFrame객체.applymap(매핑 함수)`

    ```python
    df = titanic.loc[:, ['age', 'fare']] # 행은 다 가져오되, 열은 'age'와 'fare'만 가져와라
    df_map = df.applymap(add_10)
    ```
    
    <span style="color:red">[참고] loc는 iloc와 달리 `.loc[0:9]` 라고 한다면 0부터 9까지 모두를 포함함.</span>

### 2) 시리즈 객체에 함수 매핑

- **데이터프레임의 각 열에 함수 매핑**

  `DataFrame객체.apply(매핑 함수, axis=0)`

- **데이터프레임의 각 행에 함수 매핑**

  `DataFrame객체.apply(매핑 함수, axis=1)`

### 3) 데이터프레임 객체에 함수 매핑

- **데이터프레임 객체에 함수 매핑**

  `DataFrame객체.pipe(매핑 함수)`

  - `pipe()` 메소드는 **함수를 연속적**으로 사용할 때 유용한 메소드

  - `pipe()` 메소드는 사용하는 함수가 반환하는 리턴값에 따라 `pipe()` 메소드가 반환하는 객체의 종류가 결정됨.

    ```python
    # 각 열의 NaN 찾기 - 데이터프레임을 전달할면 데이터프레임 변환
    def missing_value(x):
        return x.isnull()
    
    # 각 열의 NaN 개수 반환 - 데이터프레임을 전달하면 시리즈 변환
    def mssing_count(x):
        return missing_value(x).sum()
    
    # 데이터프레임의 총 NaN 개수 - 데이터프레임을 전달하면 값 반환
    def total_number_missing(x):
    	return missing_count(x).sum()
    ```

<br>

## 2. 열 재구성

- **열 순서 변경**
  - `DataFrame객체[재구성한 열 이름의 리스트]`

- **열 분리**
  - 데이터프레임 예) `dates = df['연월일'].str.split('-')`
  - 시리즈 예) `Series객체.str.get(인덱스)` :point_right:  `dates.str.get(0)`

<br>

## 3. 필터링

### 1) 불린 인덱싱

- **데이터프레임의 불린 인덱싱**
  - `DataFrame객체[불린 시리즈]` :point_right: `condition = (titanic.age >= 20) & (titanic.age < 30)`

### 2) isin() 메소드 활용

- **isin() 메소드를 활용한 필터링**
  - `DataFrame 열 객체.isin(추출 값의 리스트)` :point_right: `titanic['sibsp'].isin([3, 4, 5])`

<br>

## 4. 데이터프레임 합치기

### 1) concat()

- **데이터프레임 연결**

  - `pd.concat(데이터프레임의 리스트)`

  - 연결되는 데이터프레임의 행 인덱스는 `join='outer'` 옵션이 기본값으로 적용됨.

### 2) merge()

- **데이터프레임 병합**
  - `pd.merge(df_left, df_right, how='inner', on=None)`
  - `how='inner'` 옵션은 어느 한 쪽에만 속하더라도 포함(합집합), `how='outer'`는 공통으로 존재하는 교집합일 경우에만 추출
  - `on=None` 옵션은 두 데이터프레임이 공통으로 속하는 모든 열을 기준(키)로 병합한다는 뜻

:point_right: **concat()과 merge()의 차이점**

- concat()이 여러 데이터프레임을 이어 붙이듯 연결하는 것이라면, merge()는 SQL의 join 명령과 비슷한 방식으로 특정 기준에 따라 두 데이터프레임을 병합하는 것

### 3) join()

- **행 인덱스 기준으로 결합**
  - `DataFrame1.join(DataFrame2, how='left')`
  - `join()`메소드는 `merge()` 함수를 기반으로 만들어졌기 때문에 기본 작동 방식이 서로 비슷하나, `join()`메소드는 **두 데이터프레임의 행 인덱스를 기준으로 결합**한다는 점에서 차이가 있음.
  - 하지만 `join()` 메소드에 대해서도 `on=keys` 옵션을 설정하면 행 인덱스 대신 다른 열을 기준으로 결합하는 것이 가능함.

<br>

## 5. 그룹 연산

### 1) 그룹 연산(분할)

- **1개의 열을 기준으로 그룹화**
  - `DataFrame객체.groupby(기준이 되는 열)` :point_right: `grouped = df.groupby(['class'])`
- **여러 열을 기준으로 그룹화** 
  - `DataFrame객체.groupby(기준이 되는 열의 리스트)` :point_right: `grouped_two = df.groupby(['class', 'sex'])`

### 2) 데이터 집계(적용-집계)

1) **데이터 집계(내장 함수)**
   - `group객체.std()`
   - 이외에도 `mean()`, `max()`, `min()`, `first()`, `last()` 등이 있음.

2) **agg() 메소드 데이터 집계**
   - `group객체.agg(매핑 함수)`
   - 집계 연산을 처리하는 사용자 정의 함수를 그룹 객체에 적용하려면 agg() 메소드를 사용해야 함.
   - 모든 열에 여러 함수를 매핑: `group객체.agg([함수1, 함수2, 함수3, ...])`
   - 각 열마다 다른 함수를 매핑: `gorup객체.agg({'열1': 함수1, '열2': 함수2, ...})`

3. **그룹 연산 데이터 변환**
   - `group객체.transform(매핑 함수)` 
   - `transform()` 메소드는 그룹 연산의 결과를 원본 데이터프레임과 같은 형태로 변형하여 정리하는 것
4. **그룹 객체 필터링**
   - `group객체.filter(조건식 함수)` :point_right: `grouped.filter(lambda x: len(x) >= 200)`
   - 그룹 객체에 filter() 메소드를 적용할 때 조건식을 가진 함수를 전달하면 **조건이 참인 그룹만** 남김.
5. **그룹 객체에 함수 매핑**
   - `group객체.apply(매핑 함수)` :point_right: `grouped.apply(lambda x: x.describe())`

<br>

## 6. 피벗

- 피벗테이블을 구성하는 4가지 요소(행 인덱스, 열 인덱스, 데이터 값, 데이터 집계 함수)에 적용할 데이터프레임의 열을 각각 지정하여 함수의 인자로 전달

- `DataFrame객체.xs(key, axis=0, level=None, drop_level=True)`

  - xs 인덱서는 멀티인덱스 객체에 대해서 하위 분류를 출력하는 메소드
  
  - `level` 옵션은 멀티인덱스에 키가 부분적으로 포함되어있는 경우, 레벨 지정을 통해 분류
  
  - `drop_level` 옵션의 기본값은 True로 필터링하는 값을 제외하고 하위 분류만 출력(False면 필터링하는 값이 있는 분류까지 포함해 출력)
  
    [참고] [하위분류반환(xs)](https://wikidocs.net/158257)
  
  ```python
  pdf3 = pd.pivot_table(df,                     # 피벗할 데이터 프레임
                        index=['class', 'sex'],   # 행 위치에 들어갈 열
                        columns='survived',       # 열 위치에 들어갈 열 
                        values=['age', 'fare'],   # 데이터로 사용할 열
                        aggfunc=['mean', 'max'])  # 데이터 집계 함수
  ```
  
  ```python
  pdf3.xs('First')                              # 행 인덱스가 First인 행을 선택
  pdf3.xs(('First', 'female'))                  # 행 인덱스가 ('First', 'female')인 행을 선택
  pdf3.xs('male', level='sex')                  # 행 인덱스의 sex 레벨이 male인 행을 선택
  pdf3.xs(('Second', 'male'), level=[0, 'sex']) # 'Second', 'male'인 행을 선택
  pdf3.xs(('mean', axis=1))                     # 열 인덱스가 mean인 데이터를 선택
  ```

<br>

# [참고 자료]

- 오승환, 『파이썬 머신러닝 판다스 데이터 분석』, 정보문화사(2019), p.218-281.
- 김태준, 『[Python 완전정복 시리즈] 2편 : Pandas DataFrame 완전정복』, 위키독스(2022), 17-01 하위분류반환 (xs).