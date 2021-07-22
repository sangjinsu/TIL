# Python Data Model

## Magic Method

- 클래스 안에 정의할 수 있는 특별한 Built-in 메소드

### 일반형

```python
print(int)
print(float)
# <class 'int'>
# <class 'float'>

print(dir(int))
print(dir(float))

n = 10
print(n + 1000)
print(n.__add__(1000))
# print(n.__doc__)

print(n.__bool__(), bool(n))
print(n.__mul__(100))
```

### 클래스 예제 1

- 클래스 간 연산 및 비교 등이 가능하도록 돕니다.

```python
class Fruit:
    def __init__(self, name, price):
        self.__name = name
        self.__price = price

    def __str__(self): # print 시 출력
        return 'Fruit Class Info : {} {}'.format(self.__name, self.__price)

    def __add__(self, other): # +
        return self.__price + other.__price

    def __sub__(self, other): # -
        return self.__price - other.__price

    def __le__(self, other): # <=
        return self.__price <= other.__price

    def __lt__(self, other): # <
        return self.__price < other.__price

    def __ge__(self, other): # >=
        return self.__price >= other.__price

    def __gt__(self, other): # >
        return self.__price > other.__price

    def __eq__(self, other): # ==
        return self.__price == other.__price

    def __ne__(self, other): # !=
        return self.__price != other.__price
```

- 사용 예시

```python
print(orange + apple)
# 4000
print(orange - apple)
# -2000
print(orange >= apple)
print(orange <= apple)
# False
# True

print(orange)
print(apple)
# Fruit Class Info : orange 1000
# Fruit Class Info : apple 3000

print(orange == apple)
print(orange != apple)
# False
```

### 클래스 예제 2

```python
class Vector(object):
    def __init__(self, x=0, y=0):
        """
        Create a vector
        v = Vector(10, 20)
        :param x: real number
        :param y: real number
        """
        self.__x, self.__y = x, y

    def __repr__(self):
        return f'Vector({self.__x}, {self.__y})'

    def __add__(self, other):
        return Vector(self.__x + other.__x, self.__y + other.__y)

    def __mul__(self, other):
        return Vector(self.__x * other, self.__y * other)

    def __truediv__(self, other): # /
        return Vector(self.__x / other, self.__y / other)

    def __floordiv__(self, other): # //
        return Vector(self.__x // other, self.__y // other)

    def __sub__(self, other): # -
        return Vector(self.__x - other.__x, self.__y - other.__y)

    def __bool__(self): # 참, 거짓 판별
        return bool(max(self.__x, self.__y))

```

-  사용예시

```python
print(Vector.__init__.__doc__)

v1 = Vector(2, 5)
print(v1)

v2 = Vector(3, 4)
print(v1 + v2) # Vector(5, 9)

print(bool(Vector(0, 0)), bool(v2)) # False True

v3 = Vector(5, 6)
print(v1 + v2 + v3) # Vector(10, 15)
```



