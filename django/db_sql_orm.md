# SQL AND ORM

## Shell 정리 및 종료

- sqlite
  - shell clear
  - .exit
- django_shell_plus
  - clear
  - exit

## 비교 

- query

  ```sqlite
  SELECT * FROM users_user;
  ```

  ```python
  User.objects.all()
  ```

- create

  ```sqlite
  INSERT INTO users_user 
  	VALUES (
          102,
          '길동',
      	'김',
      	100,
      	'경상북도',
      	'010-1234-1234',
      	100);
  ```

  ```python
  User.objects.create(
  	first_name='길동',
      last_name='홍',
      age=100,
      country='제주도',
      phone='010-1234-5678',
      balance=10000
  )
  ```

- query by id

  ```sql
  SELECT *
  FROM users_user
  WHERE id = 102;
  ```

  ```python
  User.objects.get(pk=102)
  ```

- update

  ```sql
  UPDATE users_user SET first_name='철수' WHERE id=102;
  SELECT * FROM users_user WHERE id=102;
  ```

  ```python
  user = User.objects.get(pk=102)
  user.last_name = '김'
  user.save()
  user.last_name  # '김'
  ```

- delete

  ```sql
  DELETE FROM users_user WHERE id=101;
  SELECT * FROM users_user WHERE id=101;
  ```

  ```python
  user = User.objects.get(pk=102)
  user.delete()
  ```

- count

  ```sql
  SELECT COUNT(*)
  FROM users_user;
  ```

  ```python
  User.objects.count()
  ```

- query in condition

  ```sql
  SELECT first_name
  FROM users_user
  WHERE age = 30;
  ```

  ```python
  User.objects.filter(age=30).values('first_name')
  ```

- check query

  ```python
  print(User.objects.filter(age=30).values('first_name'))
  ```

- 대소 관계 비교 조건

  `__gte`, `__gt`, `__lte`, `__lt`

- count in condition

  ```sql
  SELECT COUNT(*)
  FROM users_user
  WHERE age >= 30;
  ```

  ```python
  User.objects.filter(age__gte=30).count()
  ```

  ```sql
  SELECT COUNT(*)
  FROM users_user
  WHERE age <= 20;
  ```

  ```python
  User.objects.filter(age__lte=20).count()
  ```

  ```sql
  SELECT COUNT(*)
  FROM users_user
  WHERE age = 30 and last_name = '김';
  ```

  ```python
  User.objects.filter(age=30).filter(last_name = '김').count()
  User.objects.filter(age=30, last_name = '김').count()
  ```

- OR

  ```sql
  SELECT COUNT(*)
  FROM users_user
  WHERE age=30 OR last_name = '김';
  ```

  ```python
  from django.db.models import Q
  User.objects.filter(Q(age=30) | Q(last_name='김')).count()
  ```

- LIKE

  ```sql
  SELECT COUNT(*)
  FROM users_user 
  WHERE phone LIKE '02-%';
  ```

  ```PYTHON
  User.objects.filter(phone__startswith='02-').count()
  ```

- values

  ```sql
  SELECT first_name
  FROM users_user 
  WHERE country='강원도' AND last_name='황';
  ```

  ```python
  User.objects.filter(country='강원도', last_name='황').values('first_name')
  ```

- order

  ```sql
  SELECT *
  FROM users_user
  ORDER BY age DESC
  LIMIT 10;
  ```

  ```python
  User.objects.order_by('-age')[:10]
  ```
  ```sql
  SELECT *
  FROM users_user
  ORDER BY balance
  LIMIT 10;
  ```

  ```python
  User.objects.order_by('balance')[:10]
  ```
    ```sql
  SELECT *
  FROM users_user
  ORDER BY balance, age DESC
  LIMIT 10;
    ```

  ```python
  User.objects.order_by('balance', '-age')[:10]
  ```
  ```sql
  SELECT *
  FROM users_user
  ORDER BY last_name DESC, first_name DESC
  LIMIT 1 OFFSET 4;
  ```

  ```python
  User.objects.order_by('-last_name', '-first_name')[4]
  ```

## Aggregation

- aggregate()
- 특정 필드 전체의 합 , 평균 , 개수 등을 계산할 때 사용

- AVG

  ```SQL
  SELECT AVG(age) 
  FROM users_user
  WHERE last_name = '김';
  ```

  ```python
  from django.db.models import Avg
  User.objects.filter(last_name = '김').aggregate(Avg('age'))
  ```

- MAX

  ```sql
  SELECT MAX(balance) 
  FROM users_user;
  ```

  ```python
  User.objects.aggregate(Max('balance'))
  ```

- MAX

  ```sql
  SELECT SUM(balance) 
  FROM users_user;
  ```

  ```python
  User.objects.aggregate(Sum('balance'))

- annotate (group by 까지 활용)

  ```sql
  SELECT country, COUNT(country) AS num_countries
  FROM users_user
  GROUP BY country;
  ```

  ```python
  User.objects.values('country').annotate(num_countries = Count('country'))
  ```
  
    ```sql
  SELECT country, COUNT(country)
  FROM users_user
  GROUP BY country;
    ```

  ```python
  User.objects.values('country').annotate(Count('country'))
  ```

  
