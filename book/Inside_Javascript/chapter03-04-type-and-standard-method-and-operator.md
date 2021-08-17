# Inside Javascript

##  Chapter03 자바스크립트 데이터 타입과 연산자

### 기본 타입과 표준 메서드

- 숫자, 문자열 같은 기본 타입은 정의된 표준 메서드들을 객체 처럼 호출할 수 있다

### 연산자

- `typeof` 연산자

  | 타입 | 타입명    | 결과           |
  | ---- | --------- | -------------- |
  | 기본 | number    | 'number'       |
  | 기본 | string    | 'string'       |
  | 기본 | boolean   | 'boolean'      |
  | 기본 | null      | 'object'       |
  | 기본 | undefined | 'undefined'    |
  | 참조 | object    | **'object'**   |
  | 참조 | array     | **'object'**   |
  | 참조 | function  | **'function'** |

- `==` 동등 연산자와 `===` 일치 연산자
  - 동등 연산자는 타입이 다른 경우 타입을 변경하여 비교한다
  - 일치 연산자는 타입을 변경하지 않고 비교한다

- `!!` 연산자
  - 피연산자를 boolean 값으로 변경한다
  - **빈 객체 ([], {})는 true 로 변환된다**

