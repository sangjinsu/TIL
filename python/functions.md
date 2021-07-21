# 함수

- 특정한 기능(역할)을 하는 코드 묶음
- 높은 재사용성, 유지보수 용이 - 단일 원칙 책임 원리 필요

- [파이썬 통계 함수](https://docs.python.org/3/library/statistics.html)

## Docstring Document String

- 함수나 클래스의 설명
- `__doc__`

## 내장 함수 Built-in Fuctions

- [내장 함수 리스트](https://docs.python.org/ko/3/library/functions.html)

## 함수 선언과 호출

- `def` 사용
- 들여쓰기로 함수  body 작성
- 매개변수 사용 가능
- return 으로 결과값 반환 - 한 객체만 가능
- 함수명()으로 호출

## 함수 input

### parameter

- parameter - [call by value or call by reference?](https://www.geeksforgeeks.org/is-python-call-by-reference-or-call-by-value/), 매개변수, 함수에 입력으로 전달된 값을 받는 변수

- parameter 로 lsit, dict, set는 함수 안에서 값 변환 주의

### argument

- argument - 전달 인자 인수, 함수를 호출할 때 함수에 전달하는 입력 값
- 가변 인자 리스트 Aribitary Argument Lists
  - 함수가 임의의 개수 인 자로 호출
  - 튜플로 처리(패킹)되고 `*args` 처럼 `*`을 붙여 사용

- 가변 키워드 인자 Arbitary Keyword Arguments

  - 딕셔너리로 처리(패킹)되고 `**kwargs` 처럼 `**`을 붙여 사용

  - 딕셔너리에 `*` 하나 사용시 키 값만 받아들임

  - ```python
    def example(**kwargs):
        pass
    example(a='a', b='b', c='c')
    ```

- 키워드 인자
  - 직접 변수 이름으로 특정 인자 전달
  - 키워드 인자 다음에 위치 인자 사용 불가

- 위치 인자
  - 기본적으로 함수 호출시 인자는 위치에 따라 함수 내부로 전달

## 함수 스코프

- local scope - 지역 스코프 : 함수 내부

- global scope - 전역 스코프 : 전체

  

- local variable - 지역 변수 : 지역 스코프에 정의된 변수

- global variable - 전역 변수 : 전역 스코프에 정의된 변수

### 변수 생명주기

- 빌트인 스코프 built-in scope

  파이썬이 실행되고 계속 유지

- 전역 스코프

  모듈이 호출된 이후나 인터프리터 종료까지 유지

- 지역 스코프

  함수 호출에 생성되고 함수 종료까지 유지

### 이름 검색 규칙 Name Resolution

- 파이썬에서 사용되는 식별자들은 namespace에 저장

  - LEGB rule

  1. local scope
  2. enclosed scope : 특정 함수의 상위 함수
  3. global scope : 함수 외부 변수, import 모듈
  4. built-in scope

- **함수 안에서 외부 스코프 변수에 접근 가능하나 수정 불가**

### global

- 현재 코드 블록 전체 적용, 전역변수
- 전역변수는 global 이전에 사용되지 않음
- 전역변수 이름은 매개변수, for 루프 대상, 클래스 및 함수 정의에 정의되면 안됨

### nonlocal

- 전역을 제외하고 가장 가까운 스코프 변수를 연결
- non-local 변수는 global 이전에 사용되지 않음
- non-local 변수 이름은 매개변수, for 루프 대상, 클래스 및 함수 정의에 정의되면 안됨
- 이미 생성된 이름과 연결만 가능

### 주의사항

1. 스코프에 변수가 없는 경우 LEGB 순서로 변수 탐색

   - 변수 수정이 불가

   - 값 할당시 새로운 변수 생성

   - 함수 내에서 필요한 상위 스코프 변수는 인자로 넘겨서 활용

     [**클로저 함수**](https://dojang.io/mod/page/view.php?id=2366)

     ```python
     def calc():
         a = 10
         b = 5
         def mul_add(x):
             return a * x + b    # 함수 바깥쪽에 있는 지역 변수 a, b를 사용하여 계산
         return mul_add          # mul_add 함수를 반환
      
     c = calc()
     print(c(1), c(2), c(3), c(4), c(5))
     ```

2. 상위 스코프에 변경하고자 하는 변수가 있다면 global, nonlocal 키워드 사용
   - 사용하지 않기를 추천
   - 내부 함수로 처리하는 것을 추천 

## 재귀함수

- 자신을 호출하는 함수, 재귀식
- 변수의 사용이 감소, 가독성이 높아짐
- 1개 이상의 base case 필요하고 수렴하도록 작성 요구

### 팩토리얼 예시

```python
def factorial(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

def factorial_recursive(n):
    if n == 1:
        return 1
    return n * factorial_resursive(n-1)
```

### 주의사항

- stack overlfow 메모리 스택이 넘는 경우
- 파이썬 최대 재귀 깊이 1000번  Recursion Error 

### 피보나치 예시

```python
def fibo(n):
    n0 = 0
    n1 = 1
    result = 1
    for i in range(n - 1):
        result = n0 + n1
        n0 = n1
        n1 = result
    return result

def fibo_recursive(n):
    if n == 1 or n == 2:
        return 1
    return fibo_recursive(n-2) + fibo_recursive(n-1)
```

