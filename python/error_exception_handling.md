# Error / Exception Handling

## 문법 에러 Syntax Error

- 줄에서 에러가 감지된 위치를 가리키는 `^ 캐럿기호`로 표시
  - `Invalid Symtax`
  - `assing to literal`
  - `EOL End of Line`
  - `EOF End of File`

## Exception

- 실행 도중 예상하지 못한 상황으로 실행 중인 프로그램이 멈춤
- 실행 중에 감지되는 에러들을 예외라고 부름
- 예외는 여러 타읍으로 나타나고 타입이 메시지에 출력
- 모든 내장 Exception은 Exception Class를 상속
- 사용자 정의 예외 생성 가능
  - `ZeroDivisionError`
  - `NameError`
  - `TypeError`
  - `TypeError` - Arguments  누락, 초과
  - `ValueError` - 타입은 올바르나 값이 적절하지 않거나 없는 경우
  - `IndexError`
  - `KeyError`
  - `ModuleNotFoundError`
  - `ImportError`
  - `KeyboardInterrupt`
  - `IdentionError`

## Exception Handling

- 순차적으로 수행됨으로, 가장 작은 범주부터 예외를 처리해야 한다.
- 마지막에 Exception을 넣어 예상치 못한 예외를 처리하도록 하자

```python
try:
    statement
except Exception as e:
    clause # 예외 발생시 실행
else:
    # try 문에서 예외가 발생하지 않으면 실행
finally:
    # 예외 발생 여부와 관계없이 항상 실행함
```

## 예외 발생 시키기

- `raise` 

  ```python
  raise Exception(message)
  # raise <표현식 (예외 타입 지정)>(메시지)
  # 예외 타입이 지정되지 않으면 현재 스코프에서 활성화된 마지막 예외 다시 발생시킴
  ```

- `assert `

  - 상태 검증에 사용, 무조건 `AssertionError` 발생
  - 일반적으로 디버깅 용도로 사용
  -  `-o` 옵션 추가시 assert 와 `__debug__`에 따른 조건부 코드 제거하고 실행

  ```python
  assert len([1, 2]) == 1, message
  # assert <표현식>, message
  # 표현식이 False인 경우 Assertion Error 발생
  ```

- [EAFP - 허락보다 용서구하는 것이 쉽다](https://wikidocs.net/16062) 

