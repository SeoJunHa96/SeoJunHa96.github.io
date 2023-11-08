---
title: Django Authentication System
date: 2023-10-04 19:06:00 +09:00
categories: [Django]
tags:
  [
    django,
    cookie,
    session,
    authentication,
    custom user model,
    login,
  ]
---

# Django Authentication System
{% raw %}
#### HTTP 특징

- 비 연결 지향(connectionless)

  서버는 요청에 대한 응답을 보낸 후 '연결을 끊음'

- 무상태(stateless)

  연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나며 상태 정보가 유지되지 않음

  로그인 상태 유지 불가



---

#### 쿠키(COOKIE)

서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각

> 클라이언트 측에서 저장되는 작은 데이터 파일이며, 사용자 인증, 추적, 상태 유지 등에 사용되는 데이터 저장 방식



- 사용 예시

  1. 브라우저가 서버에 웹 페이지를 요청
  2. 서버가 페이지와 쿠키를 보낸다.
  3. 브라우저가 다른 페이지를 같은 서버에 요청한다.

  - 같은 서버에 다른 페이지로 재요청시마다 받고 저장해 놓았던 쿠키를 함께 전송



- 쿠키 사용 원리

  브라우저(클라이언트)는 쿠키를 KEY-VALUE의 데이터 형식으로 저장

  이렇게 쿠키를 저장해 놓았다가, 동일한 서버에 재요청 시 저장된 쿠키를 함께 전송

  쿠키는 두 요청이 동일한 브라우저에서 들어왔는지 아닌지를 판단할 때 주로 사용됨

  - 이를 이용해 사용자의 로그인 상태 유지
  - 무상태 HTTP 프로토콜에서 상태 정보를 기억 시켜 주기 때문



- 사용 목적

  1. 세션 관리

     로그인, 아이디 자동 완성, 팝업 체크, 장바구니 등의 정보 관리

  2. 개인화

     사용자 선호, 테마 등의 설정

  3. 트래킹

     사용자 행동을 기록 및 분석



- 세션

  서버 측에서 생성되어 클라이언트와 서버 간의 상태를 유지

  상태 정보를 저장한는 데이터 저장 방식

  > 쿠키에 세션 데이터를 저장하여 매 요청시마다 세션 데이터를 함께 보냄



- 세션 작동 원리
  1. 클라이언트가 로그인을 하면 서버가 session 데이터를 생성 후 저장
  2. 생성된 session 데이터에 인증 할 수 있는 session id를 발급
  3. 발급한 session id를 클라이언트에게 응답
  4.  클라이언트는 응답 받은 session id를 쿠키에 저장
  5. 클라이언트가 다시 동일한 서버에 접속하면 요청과 함께 쿠키(session id가 저장된)를 서버에 전달
  6. 쿠키는 요청 때마다 서버와 함께 전송되므로 서버에서 session id를 확인해 로그인 되어있다는 것을 알도록 함



- 서버측에서 세션 데이터를 생성 후 저장하고 세션 id를 생성
- 이 ID를 클라이언트 측으로 전달하여, 클라이언트는 쿠키에 이 ID를 저장
- 서버로부터 쿠키를 받아 브라우저에 저장하고, 클라이언트가 같은 서버에 재요청 시마다 저장해 두었던 쿠키도 요청과 함께 전송
- 예를 들어, 로그인 상태를 유지하기 위해 로그인 되어있다는 사실을 입증하는 데이터를 매 요청마다 계속해서 보내는 것

- 쿠키와 세션의 목적 : 서버와 클라이언트 간의 상태를 유지



---

#### Session in Django

- 'database-backed sessions' 저장 방식을 기본 값으로 사용
- session 정보는 DB의 django_session 테이블에 저장
- Django는 특정 session id를 포함하는 쿠키를 사용해서 각각의 브라우저와 사이트가 연결된 session을 알아냄



---

#### Django Authentication System

사용자 인증과 관련된 기능을 모아 놓은 시스템(인증 시스템)



- Authentication(인증)

  사용자가 자신이 누구인지 확인하는 것 (신원 확인)



- 사전 준비

  - 두 번째 app accounts 생성 및 등록
  - auth와 관련한 경로나 키워드들을 django 내부적으로 accounts라는 이름으로 사용하고 있기 때문에 되도록 'accounts'로 지정하는 것을 권장

  ```python
  # accounts/urls.py
  from django.urls import path
  form . import views
  
  app_name = 'accounts'
  urlpatterns = [
      
  ]
  ```

  ```python
  # crud/urls.py
  
  urlpatterns = [
      ...,
      path('accounts/', include('accounts.urls')),
  ]
  ```



---

#### Custom User Model

- django가 기본적으로 제공하는 User model은 내장된 auth 앱의 User클래스를 사용

- User클래스를 대체하는 이유

  개발자가 직접 수정할 수 있도록 하기 위해

- 대체 과정

  1. AbstractUser를 상속받는 커스텀 User 클래스 작성

     기존 User클래스도 AbstractUser를 상속받기 때문에 커스텀 User클래스도 기존 User클래스와 완전히 같은 모습을 가지게 됨

     ```python
     # accounts/models.py
     
     from django.contrib.auth.models import AbstractUser
     
     class User(AbstractUser):
         pass
     ```

  2. django 프로젝트가 사용하는 기본 user 모델을 우리가 작성한 user 모델로 수정

     ```python
     # settings.py
     
     AUTH_USER_MODEL = 'accounts.User'
     ```

  3. 기본 User 모델이 아니기 때문에 등록하지 않으면 admin site에 출력되지 않음

     ```python
     # accounts/admin.py
     
     from django.contrib import admin
     from django.contrib.auth.admin import
     UserAdmin
     from .models import User
     
     admin.site.register(User, UserAdmin)
     ```

  > 프로젝트 중간에 AUTH_USER_MODEL을 변경할 수 없기 때문에 최초의 makemigration 하기 전에 할 것



---

#### Login

session을 create하는 과정



- AuthenticationForm()

  로그인 인증에 사용할 데이터를 입력 받는 built-in form

  

- 로그인 페이지 작성

  ```python
  # accounts/urls.py
  
  app_name = 'accounts'
  urlpatterns = [
      path('login/', views.login, name = login)
  ]
  ```

  ```html
  <!-- accounts/login.html -->
  
  <h1>로그인</h1>
  <form action="{% url 'accounts:login' %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  ```

  ```python
  # accounts/views.py
  
  from django.contrib.auth.form import AuthenticationForm
  
  def login(request):
      if request.method == 'POST':
          pass
      else:
          form = AuthenticationForm()
      context = {
          'form': form,
      }
      return render(request, 'accounts/login.html', context)
  ```

  

- 로그인 로직

  ```python
  # accounts/views.py
  
  from django.shortcuts import render, redirect
  from django.contrib.auth import login as auth_login
  
  def login(request):
      if request.method == 'POST':
          form = AuthenticationForm(request, request.POST)
          if form.is_valid():
              auth_login(request, form.get_user())
              return redirect('articles:index')
      else:
          form = AuthenticationForm()
      context = {
          'form': form,
      }
      return render(request, 'accounts/login.html', context)
  ```



- login(request, user)

  AuthenticationForm을 통해 인증된 사용자를 로그인 하는 함수



- get_user()

  AuthenticationForm의 인스턴스 메서드

  유효성 검사를 통과했을 경우 로그인 한 사용자 객체를 반환



- 로그인 링크

  ```html
  <!-- articles/index.html-->
  
  <h1>Articles</h1>
  <a href="{% url 'accounts:login' %}">Login</a>
  <a href="{% url 'articles:create' %}">NEW</a>
  <hr>
  ```

  

---

#### Logout

Session 을 Delete하는 과정

- logout(request)

  현재 요청에 대한 Session Data를 DB에서 삭제

  클라이언트의 쿠키에서도  Session Id를 삭제



- 로직

  ```python
  # accounts/urls.py
  
  urlpattenrs = [
      path('login/' views.login, name='login'),
      path('logout/' views.logout, name='logout'),
  ]
  ```

  ```html
  <!-- articles/index.html-->
  
  <h1>Articles</h1>
  <a href="{% url 'accounts:login' %}">Login</a>
  <form action="{% url 'accounts:logout' %}" method="POST">
    {% csrf_token %}
    <input type="submit" value="Logout">
  </form>
  ```

  ```python
  # accounts/views.py
  
  from django.contrib.auth import logout as auth_logout
  
  def logout(requets):
      auth_logout(request)
      return redirect('articles:index')
  ```

  

---

#### Template with Authentication data

템플릿에서 인증 관련 데이터를 출력하는 방법



- 현재 로그인 되어있는 유저 정보 출력

  ```html
  <!-- articles/index.html -->
  
  <h3>Hello, {{ user.username }}</h3>
  ```



- context processors

  템플릿이 렌더링 될 때 호출 가능한 컨텍스트 데이터 목록

  작성된 컨텍스트 데이터는 기본적으로 템플릿에서 사용 가능한 변수로 포함됨

  즉, django에서 자주 사용하는 데이터 목록을 미리 템플릿에 로드 해 둔 것


{% endraw %}
---

#### 참고

- AbstractUser class

  관리자 권한과 함께 완전한 기능을 가지고 있는 User model을 구현하는 추상 기본클래스



- Abstract base classes (추상 기본 클래스)

  몇 가지 공통 정보를 여러 다른 모델에 넣을 때 사용하는 클래스

  데이터베이스 테이블을 만드는 데 사용되지 않으며, 대신 다른 모델의 기본 클래스로 사용되는 경우 해당 필드가 하위 클래스의 필드에 추가 됨