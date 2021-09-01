# Django Model

## Model

- 단일 데이터 정보를 가진다

  - 사용자가 저장하는 데이터들의 필수적인 필드와 동작들을 포함

  - django는 모델을 통해 데이터에 접속하고 관리한다

  

## Database

- 스키마
  - 데이터베이스에서 자료 구조, 표현 방법, 관계 등을 정의한 구조

- 테이블
  - 행, 속성, 필드
  - 열, 튜플, 레코드 
  - 행열 모델을 사용해 조직된 데이터 요소들의 집합니다
  - 릴레이션이라고도 불린다

- 기본키
  - 각 행의 고유한 값으로 Primary Key로 불린다
  - 반드시 설정해야 하며 중복 및 null 을 설정할 수 없다
  - 유일성, NOT NULL

## ORM

- Object Relational Mapping
- 객체 지향 프로그래밍 언어를 사용하여 호한되지 않는 유형의 시스템 간의 데이터를 변환하는 프로그래밍 기술이다
- 장점
  - SQL 을 알지 못해도 DB 조작 가능
  - SQL 절차적 접근이 아닌 객체 지향적 접근
  - **<u>웹 개발 속도를 높여 생산성을 향상시킨다</u>**

- 단점
  - ORM 만으로 완전한 서비스를 구현하기 어려운 경우가 있다 

---

- 필드 모델

  - `CharField(max_length=None, **options)`
    - 길이 제한, 필드의 최대 길이(문자)

  - `TextField(**options)`
    - 글자 수가 많은 경우 
    - max_length 옵션 작성시 자동 양식 필드인 textarea 위젯에 반영 되지만 모델과 데이터베이스 수준에는 적용되지 않는다 (CharField 사용)

## Migrations

- django가 model 에 생긴 변화를 반영하는 방법
- Migration 실행 및 DB 스키마를 다루기 위한 몇가지 명령어
  - <u>makemigrations</u> - model을 변경한 것에 기반한 새로운 마이그레이션을 만들 때 사용
  - <u>migrate</u> - 마이그레이션을 DB에 반영, 설계도를 실제 DB에 반영하는 과정
  - sqlmigrate - 마이그레이션에 대한  SQL 구문 확인
  - showmigrations - 프로그램 전체 마이그레이션 상태 확인

### DateField's options

- auto_now_add 
  - 최초 생성 일자
  - 최초 삽입 시에만 현재 날자와 시간으로 갱신

- auto_now
  - 최종 수정 일자
  - 저장할 때마다 현재 날자와 시간으로 갱신 

## DB API

- django 가 기본적으로 ORM 을 제공함에 따른 것으로 DB를 편하게 조작할 수 있도록 돕는다

  `Article.objects.all()`

- Manager 
  - django 모델에 데이터베이스 query 작업이 제공되는 인터페이스
  - 기본적으로 모든 django 모델 클래스에 objects 라는 Manager 를 추가

- QuerySet
  - 데이터베이스로부터 전달 받은 객체 목록
  - queryset 안의 객체는 0개, 1개 혹은 여러 개일 수 있음
  - 데이터베이스로부터 조회, 필터, 정렬 등을 수행한다 

## Django Shell

- `pip install ipython django-extentions` 필요
- settings.py 등록 : 'django_extentions'
- `python manage.py shell_plus` 실행

## CRUD

- read

  `Article.objects.all()`

- save
  - 모델을 인스턴스화 하는 것은 DB에 영향을 미치지 않기 때문에 반드시  save()가 필요하다

- `__str__` method
  - 각각의 object가 사람이 읽을 수 있는 문자열을 반환하도록 할 수 있다
  - 작성 후 반드시 shell_plus 를 재시작해야 반영된다

- `Article.objects.get()`
  - 주어진 lookup 매개변수와 일치하는 객체를 반환한다
  - 객체가 존재하지 않으면 `DoesNotExist` 예외를 발생시킨다
  - 둘 이상의 객체이면 `MultipleObjectReturned` 예외를 발생 시킨다
  - primary key 로 검색하는 것이 절절하다

- `Article.objects.filter()`
  - lookup 매개변수와 일치하는 객체를 포함하는 새 QuerySet 을 반환한다

- update
  - 인스턴스 객체의 변수 값 변경후 저장한다

- delete
  - QuerySet 의 모든 행에 대해 SQL 삭제 쿼리를 수행하고 삭제된 객체 수와 객체 유형당 삭제 수가 포함된 딕셔너리를 반환한다

