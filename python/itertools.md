# itertools package


1.  concurrency 병행성 : 한 컴퓨터가 여러 일을 동시에 수행 -> 단일 프로그램 안에서 여러 일을 해결
2.  parallelism 병렬성 : 여러 컴퓨터가 여러 작업을 동시에 수행 -> 속도

```python
def generator_ex1():
    print('Start')
    yield 'A Point'
    print('Continue')
    yield 'B Point'
    print('End')
    
for v in temp:
    print(v)
# for in 사용시 예외가 발생하지 않음
# Start
# A Point
# Continue
# B Point
# End

temp2 = [x * 3 for x in generator_ex1()] # 리스트
temp3 = (x * 3 for x in generator_ex1()) # 튜플
# temp2 출력:
# Start
# Continue
# End
# ['A PointA PointA Point', 'B PointB PointB Point']

# temp3 출력
# <generator object <genexpr> at 0x00000267025F9A50>
for i in temp3:
    print(i)
# Start
# A Point
# Continue
# B Point
# End
```

## itertools

`import itertools`

#### count

```python
gen1 = itertools.count(1, 2.5)

print(next(gen1))
print(next(gen1))
print(next(gen1))
print(next(gen1))
# 1
# 3.5
# 6.0
# 8.5
# 무한
```

### takewhile

```python
gen2 = itertools.takewhile(lambda n : n < 10, itertools.count(1, 2.5))

for v in gen2:
    print(v)
# 1
# 3.5
# 6.0
# 8.5
```

### filterfalse 필터 반대

```python
gen3 = itertools.filterfalse(lambda n : n < 3, [i for i in range(1, 11)])

for v in gen3:
    print(v)

# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10

gen10 = itertools.filterfalse(lambda n: n % 2, [i for i in range(1, 11)])

for v in gen10:
    print(v)

    
# 2
# 4
# 6
# 8
# 10
```

### accumulate

```python
gen4 = itertools.accumulate([x for x in range(1, 101)])
for v in gen4:
    print(v)
# 1
# 3
# 6
# 10
# 15
# 21
# 28
# ....
```

### chain

```python
gen5 = itertools.chain('ABCDE', range(1, 11, 2))
print(list(gen5))
# ['A', 'B', 'C', 'D', 'E', 1, 3, 5, 7, 9]

gen6 = itertools.chain(enumerate('ABCDE'))
print(list(gen6))
# [(0, 'A'), (1, 'B'), (2, 'C'), (3, 'D'), (4, 'E')]
```

### product

```python
gen7 = itertools.product('ABCDE')
print(list(gen7))
# [('A',), ('B',), ('C',), ('D',), ('E',)]

gen8 = itertools.product('ABC', repeat=2)
# 경우의 수
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
print(list(gen8))
```

### groupby

```python
gen9 = itertools.groupby('AABBCCDDEEEE')
for char, group in gen9:
    print(f'{char} : {list(group)}')

# A : ['A', 'A']
# B : ['B', 'B']
# C : ['C', 'C']
# D : ['D', 'D']
# E : ['E', 'E', 'E', 'E']
```

