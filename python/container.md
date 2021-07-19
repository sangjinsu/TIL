# 컨테이너

- sequence 형: 순서가 있는 데이터
  - 정렬 X
  - list, tuple, range, string, binary
- non-sequence 형: 순서가 없는 데이터
  - set, dictionary

## Sequence

### list

- 인덱스로 접근
- list(), [] 로 생성
- 서로 다른 타입 데이터 저장 가능

### tuple

- immutable 

- 인덱스로 접근

- tuple(), ()로 생성

- 함수에서 복수의 값을 반환하는 경우 활용

  ```python
  t1 = (1, ) # 쉼표 주의
  ```

### range

- 숫자 시퀀스 생성에 사용
- range(n) : 0 ~ n-1
- range(n, m) : n ~ m-1
- range(n, m, step) : n ~ m-1 까지 step 증가

 ## Sequence 연산자 및 함수

- `in, not in` -  시퀀스 포함 여부 확인
- `+` - 시퀀스 간의 연결, range는 안됨
- `*` - 시퀀스 반복, range 안됨
- 인덱싱, 슬라이싱
- `len()` - 길이
- `min() max()` - 최소 최대

- `count` - 개수

  ```python
  [1, 2, 3, 3, 3].count(3)
  # 3
  ```

## non-sequence

### Set

- 순서가 없음
- set(), {} 로 생성
- set() 을 활용
- 집합 연산 가능 `|`: 합집합 `&` : 교집합 `-`: 차집합
- 중복 값 없음

### Dictionary

- key, value 쌍 자료구조
- dict(), {}로 생성
- key는 immutable 만 가능 - string, integer, float, boolean, tuple, range

### contianer 분류

- immutable - range, tuple, Number, String, Boolean
- mutable - list, set, dict