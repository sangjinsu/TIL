# 클로저 심화

클로저: 외부에서 호출된 함수의 변수값, 상태(참조) 복사 후 저장 -> 후에 접근 가능

## 클로저 사용 예제 : 클래스 -> 함수

```python
class Averager():
    def __init__(self):
        self.__series = []

    # 함수로 호출 가능
    def __call__(self, *args):
        self.__series.extend(args)
        print(f'inner => {self.__series} / {len(self.__series)}')
        return sum(self.__series) / len(self.__series)


def closure_ex1():
    # Free valuable
    # closure scope
    series = list()

    def averager(*args):
        series.extend(args)
        print(f'inner => {series} / {len(series)}')
        return sum(series) / len(series)

    return averager


print(avg_closure1(10))
print(avg_closure1(20, 30, 40, 50))
```

## function inspection

```python
print(dir(avg_closure1))
# ['__annotations__', '__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__',
# '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__get__', '__getattribute__', '__globals__', '__gt__',
# '__hash__', '__init__', '__init_subclass__', '__kwdefaults__', '__le__', '__lt__', '__module__', '__name__',
# '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__',
# '__str__', '__subclasshook__']
print(dir(avg_closure1.__code__))
# ['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__',
# '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__ne__', '__new__', '__reduce__',
# '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'co_argcount',
# 'co_cellvars', 'co_code', 'co_consts', 'co_filename', 'co_firstlineno', 'co_flags', 'co_freevars',
# 'co_kwonlyargcount', 'co_lnotab', 'co_name', 'co_names', 'co_nlocals', 'co_posonlyargcount', 'co_stacksize',
# 'co_varnames', 'replace']

print(avg_closure1.__code__.co_freevars)
# 자유변수
# ('series',)

print(avg_closure1.__closure__[0].cell_contents)
# [10, 20, 30, 40, 50]
```

## 잘못된 클로저 사용

- `nonlocal`, `global` 사용은 가독성을 저하시키고 시스템 오류를 발생시킬 여지가 많으므로 사용을 가급적 자제한다.

```python
# 잘못된 closure use case
# def closure_ex2():
#     # Free variable
#     cnt = 0
#     total = 0
#
#     def averager(v):
#         cnt += 1   # 에러 발생
#         total += v # 에러 발생
#         return total / cnt
#
#     return averager

def closure_ex2():
    # Free variable
    cnt = 0
    total = 0

    def averager(v):
        nonlocal cnt, total
        cnt += 1  # 에러 발생
        total += v  # 에러 발생
        return total / cnt

    return averager
```

