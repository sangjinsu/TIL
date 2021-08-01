# Decorator

1. 데코레이터 장점
   - 중복 제거
   - 코드 간결성
   - 공통 함수 작성
   - 로깅, 프레임워크, 유효성 체크

2. 데코레이터 단점
   - 가독성
   - 특정 기능에 한정된 함수는 단일 함수로 작성이 유리
   - 디버깅

## 실습

### 시간 측정 클로저 (데코레이터)

```python
import time
from operator import add, mul
from functools import reduce


def time_checker(func):
    def time_checked(*args):
        start = time.perf_counter()
        result = func(*args)
        end = time.perf_counter()

        name = func.__name__
        arg_str = ', '.join(repr(arg) for arg in args)

        print('[%0.5fs] %s(%s) => %r' % (end - start, name, arg_str, result))
        return result

    return time_checked

```

#### 데코레이터를 사용하지 않는 경우

```python
def func1(n):
    return reduce(mul, range(1, n))


def func2(n):
    return reduce(add, range(1, n))


none_deco1 = time_checker(func1)
none_deco2 = time_checker(func2)

print(none_deco1, none_deco1.__code__.co_freevars)
print(none_deco2, none_deco2.__code__.co_freevars)
# <function time_checker.<locals>.time_checked at 0x00000154139B9CA0> ('func',)
# <function time_checker.<locals>.time_checked at 0x00000154139B9D30> ('func',)

none_deco1(1000)
none_deco2(1000)
```

#### 데코레이터를 사용하는 경우

```python
@time_checker
def func3(n):
    return reduce(mul, range(1, n))


@time_checker
def func4(n):
    return reduce(add, range(1, n))


func3(1000)
func4(1000)
```

