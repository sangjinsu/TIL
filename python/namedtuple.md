# namedtuple

- 이번 예시는 점(포인트)과 점 사이의 거리를 구하는 식에서 포인트를 어떻게 할 것인가이다.

## 일반 튜플

- `pt1` 과 같이 일반 튜플의 경우 개발자가 이해하지 못하고 수정할 수도 있음

```python
pt1 = (1.0, 5.0)
pt2 = (2.5, 1.5)
length1 = sqrt((pt1[0] - pt2[0]) ** 2 + (pt1[1] - pt2[1]) ** 2)
```

## 네임드 튜플

- 명확하게 클래스 형태로 튜플을 제시하여 개발자가 이해하기 쉽도록 함

```python
from collections import namedtuple

Point = namedtuple('Point', 'x y')
pt3 = Point(1.0, 5.0)
pt4 = Point(2.5, 1.5)

length2 = sqrt((pt3.x - pt4.x) ** 2 + (pt3.y - pt4.y) ** 2)
```

- 인덱싱이 아닌 `key` 로 `value` 에 접근이 가능

### 네임드 튜플 선언 방법

```python
Point1 = namedtuple('Point1', ['x', 'y'])
Point2 = namedtuple('Point2', 'x, y')
Point3 = namedtuple('Point3', 'x y')
Point4 = namedtuple('Point4', 'x y x class', rename=True)
```

>  `Point4` 의 경우 원래 중복 키나 예약어 사용시 에러가 발생한다. 하지만 rename 을 True로 하면 사용이 가능하다. 그리고 난수 형태로 키 값을 생성하게 된다.

### 네임드 튜플 객체 생성

```python
p1 = Point1(x=10, y=35)
p2 = Point2(10, 35)
p3 = Point3(15, y=55)
p4 = Point4(10, 20, 30, 40)
# Point4(x=10, y=20, _2=30, _3=40)
```

### Dictionary to unpacking and unpacking

- `unpacking` 을 사용하여 딕셔너리 형태를 네임드 튜플에 넣을 수 있다.
- 네임드튜플을 `unpacking` 하여 값을 할당할 수 있다

```python
d = {'x': 75, 'y': 650}

p5 = Point1(**d)

x, y = p5
```

#### `_make()` ,  `_fields`, `_asdict()`

- `_make()` 는 리스트나 튜플을 사용해 새로운 객체를 생성한다.
- `_fields`는 필드 네임, 즉 키 값을 조회한다.
- `_asdict()` 는 OrderedDict를 반환한다. 

### 사용 예시

```python
numbers = [str(n) for n in range(1, 16)]
ranks = 'A B C D E'.split()

# list Comprehension
students = [Classes(rank, number) for rank in ranks for number in numbers]

#추천: 더 직관적임
students2 = [Classes(rank, number)
             for rank in ranks
                 for number in numbers
             ]
```



