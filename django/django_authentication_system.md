# Authentication System

- Django 인증 시스템은 django.contrib.auth 에 Django contrib 모듈로 제공된다
- 인증과 권한 부여를 제공한다

- Authentication 인증 : 신원 확인
- Authorization 권한 허가 : 권한 부여, 인증된 사용자가 수행할 수 있는 작업을 결정 

- auth 와 관련해 django 내부적으로 accounts 라는 이름으로 사용되기 때문에 accounts 로 지정하는 것을 권장한다 

## 쿠키와 세션

### HTTP

- Hyper Text Transfer protocol

- 비연결지향 (connectionless)
  - 서버는 요청에 대한 응답을 보낸 후 연결을 끊음

- 무상태 (stateless)
  - 연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나고 상태 정보가 유지되지 않는다
  - ***클라이언트와*** 서버가 주고 받는 메시지들은 완전 독립적이다

- 클라이언트와 서버의 지속적인 관계 유지를 위해 쿠키와 세션이 존재한다 

### 쿠키

- 서버가 사용자의 웹브라우저에 전송하는 데이터 조각
- 사용자가 웹사이트를 방문할 대 해당 웹사이트의 서버를 통해 사용자 컴퓨터에 설치되는 작은 기록 정보 파일
  - ***<u>클라이언트는 쿠키를 로컬에 key-value 데이터 형식으로 저장한다</u>***
  - ***<u>쿠키를 저장해 놓았다가 동일한 서버에 재요청시 저장된 쿠키를 함께 전송한다</u>*** 

- ***쿠키를 훔쳐서 사용자 계정 접근 권한을 획득하는 공격이 있다***
- HTTP 쿠키는 상태가 있는 세션을 만든다
- 쿠키는 두 요청이 동일한 브라우저에서 들어왔는지 아닌지를 판단할 대 주로 사용한다
  -  **사용자 로인 상태를 유지한다**
  - **상태가 없는 HTTP 프로토콜에서 상태 정보를 기억 시킨다**

- 웹 페이지 접속시 요청한 웹 페이지를 받으며 쿠키를 저장하고 클라이언트가 같은 서버에 재요청시 요청과 함께 쿠키도 함께 전송한다 

#### 쿠키 사용 목적

1. 세션 관리 session management
   - 로그인, 아이디 자동 완성, 공지 하루 안보기, 팝업 체크, 장바구니 정보 관리

2. 개인화 personalization
   - 사용자 선호, 테마 등의 설정

3. 트래킹
   - 사용자 행동을 기록 및 분석 

### 세션

- 사이트와 특정 브라우저 사이의 상태를 유지시키는 것

- 클라이언트가 서버에 접속하면 서버가 특정 session id 를 발급하고 

  클라이언트가 발급 받은 session id를 쿠킥에 저장

  - 클라이언트가 다시 서버에 접속하면 요청과 함께 쿠키(session id가 저장된) 를 서버에 전달
  - 쿠키를 요청 대마다 서버에 함께 전송되므로 서버에서 session id 를 확인해 알맞은 로직을 처리한다

- ID 는 세션을 구별하기 위해 필요하며 쿠키에는 ID 만 저장한다 

  

## 쿠키 수명

1. session cookies
   - 현재 세션이 종료되면 삭제됨
   - 브라우저가 현제 세션이 종료되는 시기를 정의한다

2. Persistent cookies
   - expires 속성에 지정된 날짜 혹은 Max-Age 속성에 지정된 기간이 지나면 삭제된다

## Session in Django

- 미들웨어를 통해 구현된다
- database-backed sessions 저장 방식을 기본 값으로 사용한다 
  - cached, file-based, cookie-based 방식으로 변경 가능

- 특정 session id를 포함하는 쿠키를 사용하여 브라우저가 연결된 세션을 알아낸다
- 세션정보는 django_session 테이블에 저장된다
- 모든 것을 세션으로 처리하려고 하면 사용자가 많을 때 서버에 부하가 발생한다 

---

## 로그인

- session 생성 로직과 같다

- Django는 우리가 session 메커니즘을 생각하지 않게끔 도움을 준다

  

### AuthenticationForm

- 사용자 로그인을 위한  form

- request를 첫번재 인자로 취한다

  #### login(request, user, backend=None)

  - 현재 세션에 연결하려는 인증되 사용자가 있는 경우
  - 사용자를 로그인하며  view 함수에서 사용된다
  - HttpRequest 객체와 User 객체가 필요하다
  - django session framework를 사용하여 세션에 user ID를 저장한다 

## 로그아웃

- session 삭제 로직과 같다

  #### logout(request)

  - HttpRequest 객체를 인자로 받고 반환 값이 없음
  - 사용자가 로그인하지 않은 경우 오류를 발생시키지 않는다
  - session data 를 DB 에서 완전히 삭제하고 클라이언트 쿠키에서도 sessionid가 삭제된다
  - 다른 사람이 웹 브라우저를 사용하여 로그인하고 사용자의 세션 데이터에 접근하는 것을 방지하기 위함이다 

## 로그인 사용자 접근 제한

- 접근 제한 2가지 방법
  - `is_authenticated` attribute: boolean
  - `login_required` decorator

### is_authenticated

- user model 속성
- 모든 User 인스턴스에 대해 항상 True인 읽기 전용 속성
  - AnonymousUser 에 대해서는 항상 False

- 사용자 인증 여부 확인
- request.user 에서 속성 사용
- 권한 permission 과 관련이 없으며 사용자 활성화 상태, 유효한 세션인지 확인할 수 없다 

### login_required 

- `settgings.LOGIN_URL` 에 설정된 문자열 기반 절대 경로로 redirect 한다
- `LOGIN_URL`  의 기본값은 '/accounts/login/'

- 사용자가 로그인 되어 있으면 정상적으로 view 함수 실행 

- 인증 성공시 사용자가 redirect 되어야하는 경로는 'next' 라는 쿼리 문자열 매개 변수에 저장된다

  `/accounts/login/?next=/articles/create/`

## next query string parameter

- 로그인이 정상적으로 진행되면 기존에 요청했던 주소로 redirect 하기 위해 마치 주소를 유지해주는 것

- 별도 처리하지 않으면 view 에 설정한 redirect 경로로 이동한다 

  ```python
  return redirect(request.GET.get('next') or 'articles:index')
  ```

  

---

## 회원가입

### UserCreationForm

- username,  password1, password2

  ```python
  @require_http_methods(['GET', 'POST'])
  def signup(request):
      if request.method == 'POST':
          form = UserCreationForm(request.POST)
          if form.is_valid():
              user = form.save()
              auth_login(request, user)
              return redirect('articles:index')
      else:
          form = UserCreationForm()
      context = {
          'form': form,
      }
      return render(request, 'accounts/signup.html', context)
  ```

## 회원 탈퇴

```python
@require_POST
def delete(request):
    if request.user.is_authenticated:
        request.user.delete()
        auth_logout(request)
    return redirect('articles:index')
```

## 회원 정보 수정

### UserChangeForm

```python
@login_required
@require_http_methods(['GET', 'POST'])
def update(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('article:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form
    }
    return render(request, 'accounts/update.html', context)
```

```python
# forms.py
from django.contrib.auth.forms import UserChangeForm
from django.contrib.auth import get_user_model


class CustomUserChangeForm(UserChangeForm):
    class Meta:
        model = get_user_model()
        fields = ('email', 'first_name', 'last_name')
```

## 비밀번호 변경

### PasswordChangeForm

```python
@login_required
@require_http_methods(['GET', 'POST'])
def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            return redirect('articles:index')
        else:
            form = PasswordChangeForm(request.user)
        context = {
            'form': form,
        }
        return render(request, 'accounts/change_password.html', context)
```

