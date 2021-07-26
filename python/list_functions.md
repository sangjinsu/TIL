# 리스트

- 순서가 있는 시퀀스, 인덱스로 접근

- mutable, ordered, iterable

## 값 추가 및 삭제

- `append(x)` - 리스트에 값을 추가함
-  `extend(iterable)` - 리스트에 iterable 항목을 추가함
-  `insert(i, x)` - index 위치에 값을 추가
- `remove(x)` - 리스트에서 값 삭제, 없는 경우 ValueError
- `pop(i)` - 정해진 위치에 있는 값을 삭제하고 값 반환, 위치 미지정시 마지막 값 삭제하고 반환  
- `clear()` - 모든 항목 삭제

 ## 탐색 및 정렬

- `index(x)` - index 값을 반환, 없는 경우 ValueError
- `count(x)` - 원하는 값의 개수 반환
- `sort()` - 리스트 정렬, None 반환, 원본 변경 없이 사용하려면 `sorted` 사용
- `reverse()` - 리스트 순서 뒤집음, None 반환, 원본 변경 없이 사용하려면 `reversed` 사용

## 리스트 복사

### 얕은 복사

```python
# 방법 1
a = [1, 2, 3, 4, 5]
b = a[:]

# 방법 2
a = [1, 2, 3, 4, 5]
b = list(a)

# 주의 사항 -> 복사하는 리스트의 원소가 주소를 참조하는 경우
a = [1, 2, [3, 4, 5]]
b = list(a)
b[2][0] = 0
# a와 b 같이 변환
```

### 깊은 복사

```python
import copy
a = [1, 2, [3, 4, 5]]
b = copy.deepcopy(a)
b[2][0] = 0
# a 가 변환되지 않음
```

## List Comprehension

- 표현식과 제어문을 통해 특정한 값을 가진 리스트 생성

```python
li1 = [n for n in range(1, 5)]
li2 = [n for n in range(1, 100) if n % 2]
```

## Built-in Function

- `map(function, iterable)` - iterable 모든 요소에 함수 적용하고 map object로 반환 

- `filter(function, iterable)` - iterable 모든 요소에 함수 적용하고 결과가 True 인 것을 filter object로 반환
- `zip(*iterables)` - iterable들을 모아 튜플을 원소로 하는 zip object 반환, iterable 길이가 다른 경우 가장 짧은 iterable을 기준으로 데이터가 엮이고 나머지는 버려진다.

