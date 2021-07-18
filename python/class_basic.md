# Class

## 클래스 구조

```python
class Car:
    """
    Car class
    Author: jinsuSang
    Date: 2021.07.17
    """

    # 클래스 변수
    # del 사용시 클래스 변수에 접근하는 것은 좋지 못하다고 생각함
    # 클래스 변수는 read only 형식을 사용하는 것을 개인적으로 추천
    car_count = 0

    def __init__(self, company, details):
        self.__company = company
        self.__details = details
        Car.car_count += 1

    def __del__(self):
        Car.car_count -= 1
        print('delete', self.car_count, Car.car_count)

    def __repr__(self):
        return 'repr: {} {}'.format(self.company, self.details)

    @property
    def company(self):
        return self.__company

    @property
    def details(self):
        return self.__details

    def instance_details(self):
        print('instance id: {}'.format(id(self)))
        print('company = {}, price = {}'.format(self.company, self.details.get('price')))
        
        
car1 = Car('KIA', {'color': 'White', 'horsepower': 400, 'price': 4000})
car2 = Car('Tesla', {'color': 'Red', 'horsepower': 600, 'price': 14000})
car3 = Car('Samsung', {'color': 'Blue', 'horsepower': 500, 'price': 5000})
```

## 접근 지정자 

python에서는 접근 지정자가 없지만 python 규약으로 이를 해결하려고 한다.

- `private` '_'  2개
- _ `protected` '_ ' 1개 

## `__str__` 과 `__repr__`

- `__str__` 사용자 레벨에서 사용하며 간단한 print에 사용된다

- `__repr__` 개발자 레벨에서 사용하며 객체 정보를 제공시 사용한다

- `__str__`이 `__repr_` 보다 우선하여 출력된다

- `__repr__` 을 명시적으로 상요하기 위해 `repr()`을 사용한다

  ```python
  print(repr(car))
  ```

## `__doc__`

```python
print(Car.__doc__)

# 출력 예시
    Car class
    Author: jinsuSang
    Date: 2021.07.17
```

- 클랙스 주석을 출력한다.

## [dir() 과 `__dict__`](https://darrengwon.tistory.com/552)

`dir(car1)`: 네임스페이스 출력, 네임스페이스란 이름들과 실제 객체들 사이의 매핑이다.

```bash

['_Car__company', '_Car__details', '__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'car_count', 'company', 'details', 'instance_details']

```

`print(car1.__dict__)` : 인스턴스가 가진 속성을 출력한다.

```bash
{'_Car__company': 'KIA', '_Car__details': {'color': 'White', 'horsepower': 400, 'price': 4000}}
```

## `__class__`

`__class__`: 어느 클래스에 속하고 있는지 id 값을 나타낸다.

## self

`self`: 인스턴스 자신의 고유값을 저장하는 예약어이다. JAVA에서는 this로 생각하면 될 듯하다.

## del

`del`: 인스턴스 삭제가 아닌 레퍼런스 주소와의 관계를 삭제하는데 사용된다. 관계를 끊은 뒤 가비지 콜렉터가 메모리를 회수하지만 언제 회수할지 모른다. 최대한 del 을 사용해 인스턴스를 삭제하는 일을 하지 않아야 한다.

```python
del car2
```

## class 변수

클래스 변수란 인스턴스들이 공유하는 클래스의 정보이다. 클래스 변수는 변경되는 값보다 read-only 형식으로 읽기 용도로만 사용하는 것이 좋다는 것이 개인적인 생각이다.

