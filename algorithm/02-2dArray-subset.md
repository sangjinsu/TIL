# 배열

## 2차원 배열

- 2차원 이상의 다차원 배열에 따라 인덱스 선언

  ```python
  for i in range(len(arr)):
      for j in range(len(arr[i])):
          arr[i][j]
  ```

  ```pythohn
  [[0]*n for _ in range(n)]
  ```

  ### 지그재그 순회

  ```python
  for i in range(len(arr)):
      for j in range(len(arr[0])):
          arr[i][j + (m-1-2*j) * (i%2)]
  ```

  ### 델타를 이용한 2차 배열 탐색
  
  ```python
  # 상하좌우
  dx = [0, 0, -1, 1]
  dy = [-1, 1, 0, 0]
  ```
  
  ### 전치 행렬
  
  ```python
  for i in range(n):
      for j in range(n):
          if i < j:
              arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
  ```
  
  

## 비트 연산자를 이용한 부분집합 생성

```python
arr = [-7, -3, -2, 5, 8]
n = len(arr)

for i in ragne(1<<n):
    for j in range(n+1):
        if i & (1<<j):
            print(arr[j])
```

