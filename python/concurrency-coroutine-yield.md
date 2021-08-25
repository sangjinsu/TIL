# 병행성 - 코루틴,  yield

- concurrency 병행성 : 한 컴퓨터가 여러 일을 동시에 수행 -> 단일 프로그램 안에서 여러 일을 해결
- parallelism 병렬성 : 여러 컴퓨터가 여러 작업을 동시에 수행 -> 속도

---

- 코루틴 : 단일 스레드, 스택 기반으로 동작하는 비동기 작업
- 스레드 : os 관리, CPU 코어에서 실시간, 시분할 비동기 작업 -> 멀티 스레드
- yield, send : 메인  루틴 <-> 서브 루틴
- 코루틴 제어, 상태, 양방향 전송

---


- 서브 루틴: 메인 루틴 호출  -> 서브 루틴에서 수행 (흐름 제어)
- 코루틴 : 루틴 실행 중 중지 -> 동시성 프로그래밍
- 코루틴 : 쓰레드에 비해 오버헤드 감소
- 스레드 : 싱글 스레드 -> 멀티 스레드 -> 복잡 -> 공유되는 자원 -> 교착 상태 발생 가능성, 컨텍스트 스위칭 비용 발생, 자원 소비 가능성 증가

## 코루틴 예제 1

```python
def coroutine1():
    print('coroutine started')
    i = yield
    print('coroutine recieved : {}'.format(i))


# 메인 루틴
cr1 = coroutine1()
print(cr1, type(cr1))
# <generator object coroutine1 at 0x000001C282519D60> <class 'generator'>
# yield 지점까지 서브루틴 실행
# next(cr1)

# 기본 전달 값 None
# cr1.send(200)
# 메인 루틴에서 서브루틴으로 값 전달
```

- 잘못된 사용

```python
cr2 = coroutine1()
cr2.send(500)

# TypeError: can't send non-None value to a just-started generator
# yield 지점 가지 서브루틴 실행이 필요하다
```

## 코루틴 상태, 예제 2


- GEN_CREATED : 처음 대기 상태
- GEN_RUNNING : 실행 상태
- GEN_SUSPENSED : yield 대기 상태
- GEN_CLOSED : 실행 완료 상태


```python
def coroutine2(x):
    print('coroutine started : {}'.format(x))
    y = yield x
    print('coroutine recieved : {}'.format(y))
    z = yield x + y
    print('coroutine recieved : {}'.format(z))


cr3 = coroutine2(10)

from inspect import getgeneratorstate

print(getgeneratorstate(cr3))
# GEN_CREATED

print(next(cr3))
print(getgeneratorstate(cr3))
# GEN_SUSPEND
print(cr3.send(200))

# StopIteration await 으로 자동 처리 3.5 버전 이상
```

## 중첩 코루틴 처리

```python
def generator1():
    for x in 'AB':
        yield x
    for y in range(1, 3):
        yield y


t1 = generator1()
print(next(t1))
print(next(t1))
print(next(t1))
print(next(t1))

t2 = generator1()
print(list(t2))
# ['A', 'B', 1, 2]
```

## from 사용

```python
def generator2():
    yield from 'AB'
    yield from range(1, 3)


t3 = generator2()
print(next(t3))
print(next(t3))
print(next(t3))
print(next(t3))
```

