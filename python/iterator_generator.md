# Iterator Generator

- 파이썬 반복 가능한 타입 `iterable`
- collections, text, list, Dict, Set, tuple, unpacking, *args

```python
# iter() 함수 호출하여 반복이 가능
t = 'ABCDEFGHIJKLMNOPQRSTQVWXYZ'

for c in t:
    print(c)

# '__next__'
w = iter(t)
print(next(w))
print(next(w))
print(next(w))

# 예외처리
while True:
    try:
        print(next(w))
    except StopIteration:
        break
```

## iterable 요소인지 확인

```python
from collections import abc

print(hasattr(t, '__iter__'))
print(isinstance(t, abc.Iterable))
```

## next

- 내부적으로 예외처리와 인덱스가 필요하다

  ```python
  lass WordSplitter:
      def __init__(self, text):
          self.__idx = 0
          self.__text = text.split(' ')
  
      def __next__(self):
          print('Called __next__')
          try:
              word = self.__text[self.__idx]
          except IndexError:
              raise StopIteration('Stopped Iteration.')
          self.__idx += 1
          return word
  
      def __repr__(self):
          return 'WordSplit(%s)' % self.__text
  
  
  wi = WordSplitter('Do today what you could do tomorrow')
  
  print(wi)
  print(next(wi))
  print(next(wi))
  print(next(wi))
  print(next(wi))
  print(next(wi))
  print(next(wi))
  ```

  

## Generator 패턴

- 지능형 리스트, 딕셔너리, 집합 -> 데이터 양 증가, 메모리 사용량 증가 -> 제너레이터 사용 권장

- 단위 실행 가능한 coroutine 구현과 연동

- 작은 메모리 조각을 사용

  ```python
  lass WordSplitGenerator:
      def __init__(self, text):
          self.__text = text.split(' ')
  
      def __iter__(self):
          for word in self.__text:
              yield word
  
      def __repr__(self):
          return 'WordSplitGenerator(%s)' % self.__text
  
  
  wg = WordSplitGenerator('Do today what you could do tomorrow')
  wt = iter(wg)
  
  print(next(wt))
  print(next(wt))
  print(next(wt))
  print(next(wt))
  print(next(wt))
  print(next(wt))
  print(next(wt))
  print(next(wt)) 
  # Do
  # today
  # what
  # you
  # could
  # do
  # tomorrow
  # StopIteration 발생
  ```

  

