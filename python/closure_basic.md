# Basic Closure

## global 선언

- `global` 키워드 사용으로 전역 변수를 함수 내부에서 사용

```python
b = 5


def func_v1(a):
    global b
    print(a)
    # 10
    print(b)
    # 5
    b = 100
    print(b)
    # 100


print('*****', b)  # 5
func_v1(10)
print('*****', b)  # 100
```



## 클로저 사용 이유


1. 서버 프로그래밍은  동시성 제어가 필요할 때가 있다.
2. 동시성을 사용할 때 메모리 공간에 여러 스레드가 공유 자원 접근하고 교착 상태  (데드 락)가 발생한다.
3. 이를 해결하기 위해 메모리를 공유하지 않고 메시지 전달로 처리 ex) Erlang 프로그래밍 언어
4. 메시지 전달을 위해 파이썬 클로저는 공유하지만 변경하지 않는 Immutable, READ ONLY 적극 사용, 함수형 프로그래밍과 연관
5. 클로저는 불변자료 구조 및 atom, STM을 사용해 멀티스레드 프로그래밍 강점을 가질 수 있고  coroutine을 활용한다.

## class -> closure 구현

- 값을 저장한 채로 함수를 사용할 수 있는 형태

```python
class Averager():
    def __init__(self):
        self.__series = []

    # 함수로 호출 가능
    def __call__(self, *args):
        self.__series.extend(args)
        print(f'inner => {self.__series} / {len(self.__series)}')
        return sum(self.__series) / len(self.__series)


averager_cls = Averager()
print(averager_cls(10))
# inner => [10] / 1
# 10.0

print(averager_cls(20))
print(averager_cls(30, 40, 50))
```

