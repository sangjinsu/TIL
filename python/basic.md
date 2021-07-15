# Python 기초

## 로또 번호 6개 추첨 코드

```python
import random

# 로또 번호 6개 추첨 코드 작성
numbers = range(1, 46)

pick = random.sample(numbers, 6)
pick.sort()

print(pick)

```

## 미세먼지 (조건문)

```python
# dust라는 변수에 100을 넣고
# dust 가
# 80보다 크면 나쁨
# 30보다 크면 보통
# 0보다 크면 좋음

dust = 100

status = '좋음'
if dust > 80:
    status = '나쁨'
elif dust > 30:
    status = '보통'

print(status)

```

# 딕셔너리 

```python
# 딕셔너리 항목 3개 이상
phone_book = dict(
    북경 = '032-5896-8532',
    교보문고 = '032-5988-4456',
    꽃집 = '032-5699-7712'
)

print(phone_book.get('꽃집'))
```

