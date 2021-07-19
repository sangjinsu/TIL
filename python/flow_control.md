# 제어문

## 조건문

- if 문은 참 거짓을 판단하는 조건식과 사용

  ```python
  if True:
      print(True)
      if True: 
          print('Nested')
      else:
          print('Nested else')
  elif False
      print(False)
  else:
      print('Else')
  ```

## 조건 표현식

- 일반적으로 조건에 따라 값을 정할 때 사용

- 삼항 연산자

  ```python
  num = 5
  odd = 'odd' if num % 2 else 'even' 
  ```

## 반복문

- while

  종료 조건 필요

- for

  iterable 객체 순회 후 종료

- 반복 제어

  break, continue, for ~ else

### enumerate

- (index, value) 튜플 객체로 반환

### else

-  끝까지 반복문을 실행한 이후에  else문 실행
- break 문으로 중단되면 실행되지 않음

### pass

- 아무것도 하지 않음
- 반복문 아니어도 사용