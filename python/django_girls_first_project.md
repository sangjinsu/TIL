# Django Girls 첫번째 프로젝트

window 환경 powershell 사용 필요, https://tutorial.djangogirls.org/ko/

## 1. 가상환경 만들기

```bash
$ python -m venv myvenv
```

## 2. 가상환경 사용하기

```bash
$ myvenv/Scripts/activate
```

## 3. pip 업그레이드, django 설치

```bash
$ python -m pip install --upgrade pip
```

```bash
$ pip install django
```

## 4. 프로젝트 만들기

```bash
$ django-admin startproject mysite .
```

## 5. 설정 

[설정 변경](https://tutorial.djangogirls.org/ko/django_start_project/#%EC%84%A4%EC%A0%95-%EB%B3%80%EA%B2%BD)

[데이터베이스 설정하기](https://tutorial.djangogirls.org/ko/django_start_project/#%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)

## 6. 실행

```bash
$ python manage.py runserver 8080
```

---

## 문제 상황

1. Error: [WinError 10013] 액세스 권한에 의해 숨겨진 소켓에 액세스를 시도했습니다
   - 포트 번호를 이미 사용 중이므로 다른 포트를 사용하여 접근 필요
2. django gitignore 필요
   - https://www.toptal.com/developers/gitignore 에서 프로젝트에 알맞는 .gitignore 생성하고 myvenv 추가하여 가상 실행 환경을 깃헙에 올리지 않도록 주의

3. django SECRET_KEY 숨기기
   - https://lhy.kr/django-secrets
   - json 파일을 사용하여 SECRET_KEY 를 숨기고 .gitignore 에 json 파일 추가 필수



