# random

## 1. random()

- `random.random()` 
  - 0~1 사이의 랜덤 **실수**를 반환함.

<br>

## 2. rand()

- `np.random.rand(n)`
  - 0~1 사이의 **실수** n개를 반환함.

<br>

## 3. randrange()

- `range(start, stop, step)`  :point_right:  `random.randrage(0, 101, 2)`
  - 0~100 사이의 **정수**를 2개씩 건너뛰어 하나를 랜덤하게 반환함.

<br>

## 4. randint()

- `random.randint(a, b)`  :point_right:  `random.randint(1, 10)`
  - 1~10 사이의(a와 b 모두를 포함) **정수 1개**를 반환함.
- `random.randint(a, b, n)`  :point_right:  `np.radom.randint(1, 10, 100)`
  - 1~9 사이의(a부터 b-1까지) 범위의 **정수** n개를 반환함.

<br>

## 5. choice()

- `random.choice('abcdefg')`
  - 랜덤하게 **하나의 원소**를 선택함.
- `np.random.chocie(a, n)` :point_right:  `np.random.choice(6, 10)`
  - 0~5 사이의(a-1) **정수** n개를 선택함.
- `np.random.choice(a, n, replace=True)` :point_right:  `np.random.choice(10, 6, replace=False)`
  - 0~9 사이의(a-1) **정수**를 **중복없이** n개 선택함.
- `np.random.choice(6, 10, p=[0.1, 0.2, 0.3, 0.2, 0.1, 0.1])`
  - 0~5 사이의 숫자를 뽑되 각 경우의 수가 발생할 확률인 p를 추가할 수 있음
  - 이때 p의 합은 반드시 1이 되어야 함.
  - 0은 0.1, 1은 0.2, 2는 0.3 3은 0.2, 4는 0.1, 5는 0.1만큼의 나올 확률을 지정해준 것임.

<br>

## 6. uniform()

- `random.uniform(a, b)`  :point_right:  `random.uniform(1, 10)` 
  - 1~9 사이의 랜덤 **실수**를 반환함. 

<br>

## 7. sample()

- `random.sample([a, b, c, ...], n)`  :point_right:  `random.sample([1, 2, 3, 4, 5], 3)` 
  - 랜덤하게 n개의 원소를 선택함.

<br>

## 8. shuffle()

- 원소의 순서를 랜덤하게 바꿈.

  ```python
  >>> items = [1, 2, 3, 4, 5]
  >>> random.shuffle(itmes)
  >>> items
  [5, 4, 2, 1, 3]
  ```

<br>
