# Python 기초

## 파이썬 코드 스타일 가이드

`PEP8` https://www.python.org/dev/peps/pep-0008/

## 주석

```python
# 주석
""" 
주석이지만 docstring에 주로 사용
"""
'''
주석이지만 docstring에 주로 사용
'''
```

## 코드 라인

실행 가능한 최소한의 코드 단위

- 한 줄에는 한 코드만 작성

## 변수

- type() - 변수 타입 확인
- id() - 변수에 할당된 값의 고유한 아이덴티티, 메모리 주소

## 할당 연산자

```python
x = y = 309
x, y = 1, 2
```

## swap

```python
x, y = 10, 20
y, x = x, y
```

## 식별자

변수, 함수, 모듈, 클래스 등을 식별하기 위한 이름

- 첫 글자 숫자 금지
- 대소문자 구별
- 영문 알파벳, `_` , 숫자
- 예약어 사용 불가

```python
import keyword

print(keyword.kwlist)
```

## 데이터 타입

- Number
  - integer - int
  - floating point number - float
  - complex number - complex

- String
- Boolean
- None

## integer

- 모든 정수 타입
- python3에서 long 타입 없음
- 매우 큰 수 일 경우 오버플로가 발생하지 않음
-  고정된 메모리가 아닌 가용 메모리 활용 ([임의 정밀도 산술 활용 블로그 글](https://mingrammer.com/translation-cpython-internals-arbitrary-precision-integer-implementation/))
- [임의 정밀도 정수 - 위키피디아(영문)](https://en.wikipedia.org/wiki/Arbitrary-precision_arithmetic)

### 진수 표현

- 2진수 `0b`
- 8진수 `0o`
- 16진수 `0x`

## float

### 부동소수점

- floating point rounding error 발생 (bit로 숫자 표현을 이유로 발생)

- 가장 근사치의 값을 저장

- [부동 소수점 산술: 문제점 및 한계](https://docs.python.org/ko/3/tutorial/floatingpoint.html)

- [파이썬에서 부동 소수점 오차 해결하기](https://blog.winterjung.dev/2020/01/06/floating-point-in-python)

  ```python
  print(3.14 - 3.02)
  # 0.1200000000000001
  ```

  ```python
  import math
  math.isclose(a, b) # 실수 비교
  ```

  ```py
  import sys
  print(abs(a - b) <= sys.float_info.epsilon)
  ```

## Complex

###  실수부와 허수부로 구성된 복소수

- 허수부를 j로 표현

  ```python
  a = 5+2j
  print(a.real) # 5.0
  print(a.imag) # 2.0
  ```

  

## String

- str 타입
- PEP8에서는 작은 따옴표 혹은 큰 다옴표 중 하나를 선택하여 유지하는 것을 권함

### [Escape Sequence](https://dojang.io/mod/page/view.php?id=2465)

- 문자열 내 특정 문자나 조작을 하기위해 활용

### String Interpolation

- %- formatting

- str.format()

- f-strings: python 3.6+

  ```python
  import datetime
  today = datetime.datetime.today()
  print(today)
  
  print(f'{today:%Y}년 {today:%m}월 {today:%d}일 {today:%H}시 {today:%M}분 {today:%S}초')
  print(f'{3.1525563:.2}')
  # 2021년 07월 19일 10시 29분 16초
  # 3.2
  ```


## Boolean

### False 변환

- 0, 0.0, (), [], {}, None

## None

값이 없음을 나타내는 NoneType

## 연산자

- 산술연산자

  - // - 몫
  - % - 나머지
  - ** - 거듭제곱
  - divmod()

- 비교연산자

  - is - 객체 아이덴티티

  - is not - 객체 아이덴티티가 아닌 경우

  - None 과의 비교

    ```python
    x = 2
    x is None
    ```

- 논리 연산자

  - `and`, `or`, `not`

  - **단축 평가 - 결과가 확실한 경우 두번째 값은 확인하지 않음**

- 복합 연산자

- Concatenation

  - `+` 는 숫자가 아닌 자료형에서 사용 가능

    리스트, OOP에서 활용

- Containment Test

  - 특정 요소가 속해 있는지 확인

    ```python
    'c' in 'car'
    ```

- identity

  ```python
  # 파이썬은 -5 ~ 256 까지 숫자 id 동일
  a, b = 5, 5
  print(id(a) is id(b)) # True
  c, d = 257, 257
  print(id(c) is id(d)) # False
  ```

### 연산자 우선순위

-  [링크](https://dojang.io/mod/page/view.php?id=2461)

## 표현식과 문장

- 표현식 - 식별자, 값, 연산자로 구성
  - `answer = 10 < 100` 에서 `10 < 100` 이 표현식
- 문장 - 파이썬이 실행 가능한 최소한의 코드 단위
  - 표현식이 아닌 문장: `del 5`
  - 'jinsu' 와 같은 한 값도 문장
  - 표현식도 문장
  - `answer = 10 < 100`은 문장

- 문장이 표현식을 내포함

