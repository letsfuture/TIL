# numpy

## 1. numpy 특징

- numpy array에는 한 가지 타입의 데이터만 저장할 수 있음.

  ```python
  a = np.array([1, 2, '3', 4])
  print(a)
  ```

  - 출력 결과는 `['1', '2', '3', '4']`로 3개의 정수와 1개의 문자가 저장도니 리스트를 배열로 변환하면 모두 같은 문자 타입으로 변환됨.

<br>

## 2. numpy array

### 1) numpy array 생성하기

- `np.arange(1, 2, 0.1)`
  - 1 이상 2 미만 구간에서 0.1 간격으로 실수 생성
- `np.linspace(1, 2, 11)`
  - 1부터 2까지 11개 구간으로 나눈 실수 생성
- `np.eye(n)`
- n × n의 단위 배열 생성
- `np.zeros(n)`
  - n개의 영벡터 생성
- `np.ones(n)`
  - n개의 일벡터 생성

### 2) numpy array 활용하기

- **numpy boolean**

  ```python
  a = np.arange(-5, 5)
  
  mask1 = abs(a) > 3       # mask1 = -4, -5, 4
  mask2 = abs(a) % 2 == 0  # mask2 = -4, -2, 0, 2, 4
  
  print(a[mask1+mask2])    # 둘 중 하나의 조건이라도 참일 경우(합집합을 출력)
  print(a[mask1*mask2])    # 두 가지 조건이 모두 참일 경우(교집합을 출력)
  
  # 출력 결과
  # [-5 -4 2 0 2 4]
  # [-4 4]
  ```

- **list to numpy**

  ```python
  test_numpy = np.array(test_list, dtype=int)
  ```

  - dtype을 사용해 type을 지정해줄 수 있음.

- **numpy to list**

  ```python
  test_list = test_numpy.tolist()
  ```

  

  
