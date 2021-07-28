# OOP

- 파이썬은 개체로 구성되어 있다.
- 개체는 특정 타입의 인스턴스이다.

## 개체 특징

- type - operator와 method가 가능한가
- attribute - 어떤 데이터를 가지는가
- method - 어떤 행동을 하는가

## is 연산자

- 동일한(identical)
- 두 변수가 동일한 객체를 가리키는 경우

```python
type(10) is int # True
type('10') is str # True
type(True) is bool # True
```

## isinstance 함수

- `isinstance(object, classinfo)`
- classinfo 가 인스턴스 이거나 서브 클래스인 경우 True
- classinfo 가 튜플인 경우 하나라도 일치하면 True
- classinfo가  type이거나  type으로 구성되지 않는 경우 TypeError 발생

## 개체

- 속성은 개체의 data

* 메서드는 특정 개체의 행동, 클래스 정의 함수

## 개체지향 프로그래밍

- 프로그램을 독립된 개체들의 묶음으로 보자고 하는 컴퓨터 프로그래밍 패러다임 중 하나이다.

- 클래스 - 개체들의 분류, 현실 세계의 추상화된 모델
- 인스턴스 - 클래스의 구현체

## self

- 인스턴스 자신을 가리킴
- 인스턴스 메서드 첫번째 인자로 정의한다

 ## [매직 메서드](https://docs.python.org/ko/3/reference/datamodel.html)

- `__init__`: 생성자
- `__del__`: 소멸자
- `__str__`: 해당 객체의 출력 형태를 지정한다.
- `__gt__`: 부등호 연산자 `>`

## 클래스와 인스턴스

### 변수

- 인스턴스 변수 - 인스턴스 개체 데이터
- 클래스 변수 - 클래스 속성으로 모든 인스턴스가 공유하는 데이터
- 인스턴스와 클래스 간의 namespace - 인스턴스 다음 클래스 순서로 변수를 탐색

### 메서드

- instance method - 클래스 내부 기본 메서드, 첫번째 인자는 `self`
- class method - `@clasmethod` 데코레이터를 사용하여 정의, 첫번째 인자는 `cls` 
- static method - `@staticmethod` 데코레이터를 사용하여 정의, 인자를 전달하지 않아 클래스 정보에 접근하거 수정을 할 수 없음

## 상속

- 클래스는 상속이 가능함
- 최상위 클래스는 object임
- 서브 클래스가 슈퍼 클래스로부터 속성과 메서드를 상속받으면서 중복을 줄이고 재사용성을 높임
- 상속을 통해 개체 사이 관계를 구성
- `isinstance(object, classinfo)`
- `issubclass(class, classinfo)`- classinfo가 튜플일 수도 있음. 모든 항복을 검사한다.
- `super()` - 서브 클래스에서 슈퍼 클래스를 사용하는 경우
- 메서드 오버라이딩 - 상속된 메서드를 재정의, 슈퍼 클래스 메서드 사용시 super() 사용
- 다중 상속ㅉ
  - 두 개 이상의 클래스를 상속 받는 경우
  - 상속 받은 모든 클래스의 요소 활용 가능
  - 중복된 속성이나 메서드가 있는 경우 상속 순서에 따라 결정됨 







