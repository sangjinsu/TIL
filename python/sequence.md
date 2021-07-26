# Sequence

- Container - 서로 다른 자료형 (`list`,` tuple`, `collections.deque`)
- Flat - 자료형 하나 (`str`, `bytes`,  `bytearray`)

- mutable - `list`, `bytearray`, `array.array`, `memoryview`, `deque`
- immutable - `tuple`, `str`, `bytes`

## Comprehending List

```python
chars = '+_)(*&^%$#@!~'
code_list2 = [ord(s) for s in chars]
# 유니코드 리스트

# Comprehending lists + map, filter
code_list3 = list(filter(lambda x: x > 40, map(ord, chars)))
```

## `array.array` 효율적인 숫자 배열

[python 공식 문서](https://docs.python.org/ko/3/library/array.html)

```
import array
arr1 = array.array('I', (ord(s) for s in chars))
print(type(arr1))
print(arr1.tolist())
```

![출처: 파이썬 공식 문서](C:/Users/sangjs/AppData/Roaming/Typora/typora-user-images/image-20210726213844632.png)

### list vs array

- 리스트 기반 : 융통성 다양한 자료형, 범용적 사용
- 숫자 기반: 배열(리스트와 거의 호환)

## list 주의사항

```python
marks1 = [['~'] * 2 for n in range(3)]
print(marks1)
marks2 = [['~'] * 2] * 3
print(marks2)

# 수정
marks1[0][1] = 'X'
print(marks1)
# [['~', 'X'], ['~', '~'], ['~', '~']]

marks2[0][1] = 'X'
print(marks2)
# [['~', 'X'], ['~', 'X'], ['~', 'X']]

# 증명
print([id(i) for i in marks1])
print([id(i) for i in marks2])
# [2920572830976, 2920572830848, 2920572830784] id 값이 다름
# [2920572830592, 2920572830592, 2920572830592] id 값이 동일함 
```

## mutable vs immutable

```python
m = (15, 20, 25)
n = [15, 20, 25]
print(m, id(m))
print(n, id(n))

m *= 2
n *= 2
print(m, id(m))  # 튜플 id 값 다름
print(n, id(n))  # 리스트 id 값 같음

# (15, 20, 25) 1528975510784
# [15, 20, 25] 1528975214848
# (15, 20, 25, 15, 20, 25) 1528975471712
# [15, 20, 25, 15, 20, 25] 1528975214848

```

## sort vs sorted

- `reverse`, `key` 옵션 활용
- `sorted` 정렬 후 새로운 객체 변환
- `sort` 정렬 후 객체 직접 변경

```python
fruits = ['orange', 'apple', 'watermelon', 'pineapple', 'kiwi']
print('sorted:', sorted(fruits))
print('sorted:', sorted(fruits, reverse=True))
print('sorted:', sorted(fruits, key=len))
print('sorted:', sorted(fruits, key=lambda x: x[-1], reverse=True))

# sorted: ['apple', 'kiwi', 'orange', 'pineapple', 'watermelon']
# sorted: ['watermelon', 'pineapple', 'orange', 'kiwi', 'apple']
# sorted: ['kiwi', 'apple', 'orange', 'pineapple', 'watermelon']
# sorted: ['watermelon', 'kiwi', 'orange', 'apple', 'pineapple']

print('sort:', fruits.sort(), fruits)
print('sort:', fruits.sort(reverse=True), fruits)
print('sort:', fruits.sort(key=len), fruits)
print('sort:', fruits.sort(key=lambda x: x[-1], reverse=True), fruits)

# sort: None ['apple', 'kiwi', 'orange', 'pineapple', 'watermelon']
# sort: None ['watermelon', 'pineapple', 'orange', 'kiwi', 'apple']
# sort: None ['kiwi', 'apple', 'orange', 'pineapple', 'watermelon']
# sort: None ['watermelon', 'kiwi', 'apple', 'orange', 'pineapple']

```

## hash()

- mutable 자료구조는 hash를 이용할 수 없다

```python
t1 = (10, 20, (30, 40, 50))
t2 = (10, 20, [30, 40, 50])

print(hash(t1))
# print(hash(t2))
```

## Dict Setdefault

> *key* 가 딕셔너리에 있으면 해당 값을 돌려줍니다. 그렇지 않으면, *default* 값을 갖는 *key* 를 삽입한 후 *default* 를 돌려줍니다. *default* 의 기본값은 `None` 입니다.

- [파이썬 공식 문서](https://docs.python.org/ko/3/library/stdtypes.html?highlight=setdefault#dict.setdefault)

```python
source = (('k1', 'val1'),
          ('k1', 'val2'),
          ('k2', 'val3'),
          ('k2', 'val4'),
          ('k2', 'val5'),)

dict1 = {}
dict2 = {}

# no use Setdefault

for k, v in source:
    if k in dict1:
        dict1[k].append(v)
    else:
        dict1[k] = [v]

# use Setdefault
for k, v in source:
    dict2.setdefault(k, []).append(v)
```

## immutable Dict

- [파이썬 공식 문서](https://docs.python.org/ko/3/library/types.html?highlight=mappingproxytype#types.MappingProxyType)

  >  매핑의 <u>**읽기 전용**</u> 프락시. 매핑 항목에 대한 동적 뷰를 제공하는데, 매핑이 변경될 때 뷰가 이러한 변경 사항을 반영함을 의미합니다.

```python
from types import MappingProxyType

d = {'k1': 'v1'}
d_frozen = MappingProxyType(d)

print(d, id(d), type(d))
print(d_frozen, id(d_frozen), type(d_frozen))
# {'k1': 'v1'} 2557747036224 <class 'dict'>
# {'k1': 'v1'} 2557747494864 <class 'mappingproxy'>

# d_frozen['k2'] = 'v2'
# 'mappingproxy' object does not support item assignment
```

## immutable Set

- [파이썬 공식 문서](https://docs.python.org/ko/3/library/stdtypes.html#frozenset)

  > *iterable* 에서 요소를 취하는 새 set 또는 frozenset 객체를 돌려줍니다. 집합의 원소는 반드시 [해시 가능](https://docs.python.org/ko/3/glossary.html#term-hashable)(immutable)해야 합니다. 집합의 집합을 표현하려면, 포함되는 집합은 반드시 frozemset 객체여야 합니다. *iterable* 을 지정하지 않으면 새 빈 집합을 돌려줍니다.

```python
s = {2, 5, 7}
s2 = {2, 7, 7, 8}
s3 = frozenset(s2)
# s3.add('melon')
# AttributeError: 'frozenset' object has no attribute 'add'
print(s, type(s))
print(s2, type(s2))
print(s3, type(s3))

# {2, 5, 7} <class 'set'>
# {8, 2, 7} <class 'set'>
# frozenset({8, 2, 7}) <class 'frozenset'>
```

## 선언 최적화 및 인터프리터 내부 작동 알아보기

- [파이썬 공식 문서](https://docs.python.org/ko/3/library/dis.html?highlight=dis#module-dis)
- [dis](https://docs.python.org/ko/3/library/dis.html?highlight=dis#module-dis) 모듈은 CPython [바이트 코드](https://docs.python.org/ko/3/glossary.html#term-bytecode)를 역 어셈블 하여 분석을 지원합니다.

- set() 보다 `{}` 선언이 빠르다.
- list comprehension 보다 map, filter 사용이 빠르다. (상황에 따라 다름)

```python
from dis import dis
print('---------')
print(dis('{10}'))
print('---------')
print(dis('set([10])'))

'''
---------
  1           0 LOAD_CONST               0 (10)
              2 BUILD_SET                1
              4 RETURN_VALUE
None
---------
  1           0 LOAD_NAME                0 (set)
              2 LOAD_CONST               0 (10)
              4 BUILD_LIST               1
              6 CALL_FUNCTION            1
              8 RETURN_VALUE
None

'''
```

```python
print('---------')
print(dis('''
chars = '+_)(*&^%$#@!~'
list(filter(lambda x: x > 40, map(ord, chars)))
'''))
print('---------')
print(dis('''
chars = '+_)(*&^%$#@!~'
[ord(x) for x in chars if ord(x) > 40]
'''))

'''
  2           0 LOAD_CONST               0 ('+_)(*&^%$#@!~')
              2 STORE_NAME               0 (chars)

  3           4 LOAD_NAME                1 (list)
              6 LOAD_NAME                2 (filter)
              8 LOAD_CONST               1 (<code object <lambda> at 0x000001D88EF6F870, file "<dis>", line 3>)
             10 LOAD_CONST               2 ('<lambda>')
             12 MAKE_FUNCTION            0
             14 LOAD_NAME                3 (map)
             16 LOAD_NAME                4 (ord)
             18 LOAD_NAME                0 (chars)
             20 CALL_FUNCTION            2
             22 CALL_FUNCTION            2
             24 CALL_FUNCTION            1
             26 POP_TOP
             28 LOAD_CONST               3 (None)
             30 RETURN_VALUE

Disassembly of <code object <lambda> at 0x000001D88EF6F870, file "<dis>", line 3>:
  3           0 LOAD_FAST                0 (x)
              2 LOAD_CONST               1 (40)
              4 COMPARE_OP               4 (>)
              6 RETURN_VALUE
None
---------
  2           0 LOAD_CONST               0 ('+_)(*&^%$#@!~')
              2 STORE_NAME               0 (chars)

  3           4 LOAD_CONST               1 (<code object <listcomp> at 0x000001D88EF6F870, file "<dis>", line 3>)
              6 LOAD_CONST               2 ('<listcomp>')
              8 MAKE_FUNCTION            0
             10 LOAD_NAME                0 (chars)
             12 GET_ITER
             14 CALL_FUNCTION            1
             16 POP_TOP
             18 LOAD_CONST               3 (None)
             20 RETURN_VALUE

Disassembly of <code object <listcomp> at 0x000001D88EF6F870, file "<dis>", line 3>:
  3           0 BUILD_LIST               0
              2 LOAD_FAST                0 (.0)
        >>    4 FOR_ITER                24 (to 30)
              6 STORE_FAST               1 (x)
              8 LOAD_GLOBAL              0 (ord)
             10 LOAD_FAST                1 (x)
             12 CALL_FUNCTION            1
             14 LOAD_CONST               0 (40)
             16 COMPARE_OP               4 (>)
             18 POP_JUMP_IF_FALSE        4
             20 LOAD_GLOBAL              0 (ord)
             22 LOAD_FAST                1 (x)
             24 CALL_FUNCTION            1
             26 LIST_APPEND              2
             28 JUMP_ABSOLUTE            4
        >>   30 RETURN_VALUE
None
'''
```

## Comprehending Set

- [unicodedata 파이썬 공식 문서](https://docs.python.org/ko/3/library/unicodedata.html?highlight=unicodedata%20name#module-unicodedata)

```python
from unicodedata import name

print({name(chr(i), '') for i in range (97, 123)})
# {'', 'LATIN CAPITAL LETTER Z', 'QUESTION MARK', 'PLUS SIGN', 'LATIN CAPITAL LETTER AE', 'LATIN SMALL LETTER A WITH TILDE', 'LATIN CAPITAL LETTER A WITH CIRCUMFLEX', 'LATIN CAPITAL LETTER Y WITH ACUTE', 'APOSTROPHE', ... ... }

```





