# Managing Static File

## Static Files

- 정적 파일

- 응답시 처리 없이 파일 내용을 그대로 보여주는 파일

- Django 에서는 이런 파일들을 static file 이라고 부른다 

  - `settings.py` 에서 STATIC_URL 정의 필요 
  - `load`: 사용자 정의 템플릿 태그 세트를 로드한다, 로드하는 라이브러리, 패키지에 등록된 모든 태그와 필터 로드
  - `static`: STATIC_ROOT 에 저장된 정적 파일에 연결한다 

  ```django
  {% load static %}
  
  <img src="{% static 'my_app/example.jpg' %}" alt='My image'>
  ```

  - `STATIC_ROOT`

    - `collectstatic` 이 배포를 위해 정적 파일을 수집하는 디렉터리의 절대 경로이다

    - django 프로젝트에서 사용하는 모든 정적 파일을 한 곳에 모아 넣는 경로

    - 배포 환경에서 django의 모든 정적 파일을 다른 웹 서버가 직접 제공하기 위함이다 

      ```python
      STATIC_ROOT = BASE_DIR / 'staticfiles'
      ```

      ```bash
      $ python manage.py collectstatic
      ```

  - `STATIC_URL`

    - `STATIC_ROOT` 에 있는 정적 파일을 참조할 때 사용할 URL

    - 개발 단계에서는 실제 정적 파일들이 저장되어 잇는 app/static/경로 및 STATICFILES_DIRS 에 정의된 추가 경로들을 탐색한다

    - 실제 파일이나 디렉토리가 아니라 URL 만 존재한다 

    - 비어 있지 않은 값 설정시 `/` 로 끝나야 한다 

      ```python
      STATIC_URL = '/static/'
      ```

  - `STATICFILES_DIRS`

    - `app/static/` 디렉터리 경로를 사용하는 것 외에 추가적인 정적파일 경로 목록을 정의하는 리스트

      ```python
      STATICFILES_DIRS = [
          BASE_DIR / 'static'
      ]
      ```

  정적 파일 경로 : `app/static/app`

  ```django
  {% extends 'base.html' %} {% load static %} {% block content %}
  <img src="{% static 'articles/sample1.jpg' %}" alt="" srcset="" />
  ```

## Media File

- 미디어 파일

- 유저가 업로드한 모든 정적 파일

- 사용자가 웹에서 업로드하는 정적 파일

  - `MEDIA_ROOT`

    - 사용자가 업로드 한 파일들을 보관할 디렉터리 절대 경로
    - django는 성능을 위해 업로드 파일을 데이터베이스에 저장하지 않는다 

    ```python
    MEDIA_ROOT = BASE_DIR / 'media'
    ```

  - `MEDIA_URL`
    - `MEDIA_ROOT` 에서 제공되는 미디어를 처리하는 URL
    - 업로드 된 파일 주소를 만들어 주는 역할
    - 비어 있지 않은 값 설정시 `/` 로 끝나야 한다 

  ```python
  rom django.contrib import admin
  from django.urls import path, include
  from django.conf import settings
  from django.conf.urls.static import static
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('articles/', include('articles.urls')),
  ] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
  ```

### Field

- `ImageField`
  - 이미지 업로드에 사용하는 모델 필드
  - `FileField` 상속하는 서브 클래스
  - 최대 길이 100자인 문자열로 DB에 생성된다 
  - `Pillow` 라이브러리가 필요하다

- `FileField`

  - 파일 업로드에 사용하는 모델 필드

  - 2개 선택 인자를 가진다

    1. `upload_to`: 업로드 디렉토리와 파일이름을 설정하는 방법 2가지 제공 

       - 문자열 값이나 경로 지정

         ```python
         // models.py
         image = models.ImageField(
                 blank=True, upload_to='images/%Y/%m/%d', height_field=None, width_field=None, max_length=None)
         ```

       - 함수 호출

         ```python
         def articles_image_path(instance, filename):
             return f'user_{instance.pk}/{filename}'
         
         image = models.ImageField(blank=True, upload_to=articles_image_path, height_field=None, width_field=None, max_length=None)
         ```

       - instance  - FileField 가 정의된 모델의 인스턴스로 데이터베이스 저장이 아니라서 `pk`를 가지지 않는다

       - filename - 기존 파일에 제공된 파일 이름 

    2. `storage`

## CREATE

- `ImagieField` 
  - upload_to='images/'
  - blank=True

#### Model field option

- blank

  - 이미지 필드에 빈 값이 허용되도록 설정한다 

  - 기본값 False 

  - True인 경우 필드를 비워둘 수 있다

    D에는 빈 문자열로 저장된다

  - 유효성 검사에서 사용된다 (is_valid)

    True 인 경우 유효성 검사에서 빈 값을 입력할 수 있다 

- null

  - 기본 값 False 

  - True 이면 django는 빈값을 DB에 NULL로 저장

  - CharField, TextField 와 같은 문자열 기반 필드에는 사용을 피해야 한다, 데이터 없음이 중복된다 

    

### form 요소 - enctype  속성

1. `multipart/form-data`
   - 파일/이미지 업로드 시에 반드시 사용해야 한다 

### input 요소 - accept 속성

1. 입력 허용할 파일 유형을 나타내는 문자열
2. 파일을 검증하는 것은 아니다
3. 쉼표로 구분된 고유 파일 유형 지정자이다

## UPDATE

- 이미지는 바이너리 데이터이므로 일부 수정이 불가하다

- 새로운 사진을 덮어 쓰기로 업데이트한다

- 이미지 존재 여부 확인 

  ```django
  {% if article.image %}
  <img
    src="{{article.image_thumbnail.url}}"
    alt="{{article.thumbnail}}"
    srcset=""
  />
  {% endif %}
  ```

## 