# Django

- 파이썬 웹 프레임워크 

## Static Web Page

- 정적 웹 페이지
- 서버에 미리 저장된 파일이 사용자에게 그대로 전달되는 웹 페이지
- 모든 상황에서 모든 사용자에게 동일한 정보를 표시
- flat page

## Dynamic web page

- 웹 페이지에 대한 요청을 받은 경우 서버는 추가적인 처리 과정 이후 클라이언트에게 응답을 보낸다
- 서버 사이드 프로그래밍 언어가 사용되며 파일 처리 및 데이터베이스를 이용한다 

## Framework

- 프로그래밍에서 특정 운영 체제를 위한 응용 프로그램 표준 구조를 구현하는 클래스와 라이브러리 모임이다
- 새로운 애플리케이션을 위한 표준 코드를 다시 작성하지 않아도 같이 사용할 수 있도록 도운다
- Application Framework 라고도 한다 

## Framework Architecture

- MVC Design Pattern

- Model - View - Controller

  - Model 

    응용 프로그램 데이터 구조를 정의하고 데이터베이스 기록을 관리

  - Template

    파일 구조나 레이아웃을 정의

    실제 내용을 보여주는 데 사용

  - View 

    HTTP 요청을 수신하고 HTTP 응답을 반환

    Model을 통해 요청을 충족시키는데 필요한 데이터에 접근

    template에게 응답의 서식 설정을 맡김

## Django

- settings.py

  - LANGUAGE_CODE

    모든 사용자에게 제공되는 번역을 결정한다

  - TIME_ZONE

    데이터베이스 연결의 시간대를 나타내는 문자열 지정

## Template

- 데이터 표현을 제어하는 도구이자 표현에 관련된 로직

- built-in system => Django template language

  ### Django Template Language

  - [built-in template Django  공식 홈페이지](https://docs.djangoproject.com/en/3.2/ref/templates/builtins/)

  - 프로그래밍 로직이 아니라 프레젠테이션을 표현하기 위한 것

    1. Variable
       - `render()`를 사용하여 views.py에서 정의한 변수를  template 파일로 넘겨 사용한다
       - `.` 을 사용하여 변수 속성에 접근한다
       - `render()` 세번째 인자로 `{key, value}`로 값을 전달한다

    2. Filter
       - 표시할 변수를 수정할 때 사용

    3. Tags
       - `{%  %}` 
       - 출력 텍스트를 만들거나, 반복 또는 논리를 수행하여 제어흐름을 만드는 등 변수보다 복잡한 일들을 수행
       - 일부 태그는 시작과 종료 태그가 필요
       - `{% if %}{% endif %}`

    4. Comments
       - `{# #}`
       - `{% comment %}주석{% endpoint %}`

  ### Django Template Inheritance

  - 템플릿 상속은 기본적으로 코드 재사용성에 초점을 맞춘다
  - 템플릿 상속을 하면 사이트의 모든 공통 요소를 포함하고 하위 템플릿을 재정의하는 과정을 가진다

  ### Django template system

  - 표현과 로직을 분리

  - 중복을 배제

    

## HTML "form" element

- 웹에서 사용자 정보를 입력하는 여러 방식 제공

- 서버로 전송하는 역할을 담당

- 핵심 속성

  - action : 입력 데이터가 전송될 URL 지정
  - method : 입력 데이터 전달 방식 지정

  ### HTML "input" element

  - 사용자 입력

  - type 속성에 따라 동작 방식이 달라짐

  - 핵심 속성

    - name: 중복 가능

    - 주요 용도는 GET/POST 방식으로 서버에 전달하는 파라미터로 name 이 key, 입력값을 value 로 사용한다 

      `?key=value&key=value`

  ### HTML "label" element

  - 사용자 인터페이스 항목에 설명을 나타낸다
  - input 에 id 속성을 부여하고 label에는 input의 id와 동일한 값의 for 속성이 필요하다

  - label 과 input 요소 연결 주요 이점
    1. 시각적인 기능과 더불어 화면 리더기에서 label을 읽어서 사용자가 입력해야 하는 텍스트가 무엇인지 더 이해하기 쉽도록 할 수 있다
    2. label을 클릭해서 input을 focus, activate 할 수 있음 

  ### HTML "for" attribute

  - for 속성 값과 일치하는 id를 가진 문서의 첫 번째 요소를 제어

  ### HTML "id" attribute

  - 고유 식별자 정의

## HTTP

- GET
  - 서버로부터 정보를 조회하는데 사용
  - Query String Parameters를 통해 전송

## URL

#### variable routing

- url 주소를 변수로 사용하는 것
- url 일부를 변수로 지정하여 view 함수 인자로 넘길 수 있다
- 변수 값에 따라 한 path() 에 여러 페이지를 연결 시킬 수 있다

#### Path Converters

- str
  - '/' 를 제외하고 비어 있지 않은 모든 문자열과 매치
  - 작성하지 않을 경우 기본 값

- int
  - 0 또는 양의 정수와 매치

