---
title: Django ORM with View
date: 2023-09-25 19:06:00 +09:00
categories: [Django]
tags:
  [
    django,
    MTV,
    orm,
    view,
    csrf,
  ]
---

# Django ORM with view
{% raw %}
#### Read(조회)

- 전체 게시글 조회

  ```python
  # articles/views.py
  from .models import Article
  
  def index(request):
      articles = Article.objects.all()
      context = {
          'articles' : articles,
      }
      return render(request, 'articles/index.html', context)
  ```

  ```html
  <!--articles/index.html-->
  
  <h1>Articles</h1>
  <hr>
  {% for article in articles %}
  	<p>글 번호: {{article.pk}}</p>
      <p>글 제목: {{article.title}}</p>
      <p>글 내용: {{article.content}}</p>
      <hr>
  {% end for %}
  ```

  

- 단일 게시글 조회

  ```python
  # articles/urls.py
  
  urlpatterns = [
      ...
      path('<int:pk>/', views.detail, name = 'detail'),
  ]
  ```

  ```python
  # articles/vies.py
  def detail(request, pk):
      article = Article.objects.get(pk = pk)
      context = {
          'article': article,
      }
      return render(request, 'articles/detail.html', context)
  ```

  ```html
  <!--templates/articles/detail.html -->
  
  <h2>DETAIL</h2>
  <h3>{{article.pk}} 번째 글</h3>
  <hr>
  <p>제목 : {{ article.title }}</p>
  <p>내용 : {{ article.content }}</p>
  <p>작성일 : {{ article.created_at }}</p>
  <p>수정일 : {{ article.updated_at }}</p>
  <hr>
  <a href="{% url'articles:index'%}">[back]</a>
  ```

  

- 단일 게시글 페이지 링크 작성

  ```html
  <!-- templates/articles/detail.html -->
  <h1>Articles</h1>
  <hr>
  {% for article in articles %}
     <p>글 번호 : {{ article.pk }}</p>
     <a href="{% url 'articles:detail' article.pk %}">
     	  <p>글 제목 : {{ article.title }}</p>
     </a>
     <p>글 내용 : {{article.content}} </p>
     <hr>
  {% end for %}
  ```

  

----

#### Create

- create 로직을 구현하기 위해 필요한 view 함수
  - 사용자 입력 데이터를 받을 페이지를 렌더링 : new
  - 사용자가 입력한 데이터를 받아 DB에 저장 : create



- new 기능 구현

  ```python
  # articles/urls.py
  urlpatterns = [
      ...
      path('new/', views.new, name='new'),
  ]
  ```

  ```python
  # articls/views.py
  
  def new(request):
      return render(request, 'articles/new.html')
  ```

  ```html
  <!-- tmplates/articles/new.html-->
  
  <h1>NEW</h1>
  <form action="#" method="GET">
    <div>
      <label for="title">Title: </label>
      <input type="text" name="title" id = "title">
    </div>
    <div>
      <label for="content">Content: </label>
      <textarea name="content" id="content"></textarea>
    </div>
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[back]</a>
  ```

  ```html
  <!-- templates/articles/index.html -->
  
  <h1>Articles</h1>
  <a herf="{% url 'articles:new' %}">NEW</a>
  <hr>
  ...
  ```

  


- create 기능 구현

  ```python
  # articles/urls.py
  
  urlpatterns = [
      ...
      path('create/', views.create, name='create'),
  ]
  ```

  ```html
  <!--templates/articles/create.html -->
  <h1>게시글이 작성 되었습니다.</h1>
  ```

  ```python
  # articles/views.py
  
  def creta(request):
      title = request.GET.get('title')
      content = request.GET.get('content')
      
      #1.
      article = Article()
      article.title = title
      article.content = content
      article.save()
      
      #2.
      article = Article(title = title, content = content)
      article.save()
      
      #3.
      Article.objects.create(title = title, content = content)
      
      return render(request, 'articles/create.html')
  
  # 3가지 다 작동은 하지만, 2번을 사용하는 것을 권장.
  ```

  ```html
  <!-- tmplates/articles/new.html-->
  
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="GET">
    <div>
      <label for="title">Title: </label>
      <input type="text" name="title" id = "title">
    </div>
    <div>
      <label for="content">Content: </label>
      <textarea name="content" id="content"></textarea>
    </div>
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[back]</a>
  ```

  

---

#### HTTP request methods

- HTTP : 네트워크 상에서 데이터를 주고 받기 위한 약속

- HTTP request methods

  데이터(리소스)에 어떤 요청(행동)을 원하는지 나타내는 것(GET & POST)



- 'GET' Method

  특정 리소스를 조회하는 요청(url에 노출됨)

  (GET으로 데이터를 전달하면 Query String 형식으로 보내짐)

  ```html
  http://127.0.01:8000/articles/create/?title=제목&content=내용
  ```



- 'POST' Method

  특정 리소스에 변경(생성, 수정, 삭제)을 요구하는 요청(조회를 뺀 나머지)

  POST로 데이터를 전달하면 HTTP Body에 담겨 보내짐(url에 노출되지 않음)



- POST method 적용

  ```html
  <!-- tmplates/articles/new.html-->
  
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
    <div>
      <label for="title">Title: </label>
      <input type="text" name="title" id = "title">
    </div>
    <div>
      <label for="content">Content: </label>
      <textarea name="content" id="content"></textarea>
    </div>
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[back]</a>
  ```

  ```python
  # articles/views.py
  
  def create(request):
      title = request.POST.get('title')
      content = request.POST.get('content')
      ...
  ```

  - 게시글 작성 후 403 응답 확인



- HTTP response status code

  특정 HTTP 요청이 성공적으로 완료되었는지를 3자리 숫자로 표현하기로 한 것

  - 403 Forbidden : 서버에 요청 전달, 권한 때문에 거절

    거절이 누락된 이유 확인



- CSRF (Cross-Site-Request-Forgery)

  사이트 간 요청 위조

  사용자가 자신의 의지와 무관하게 공갹자가 의도한 행동을 하여, 특정 웹 페이지를 보안에 취약하게 하거나 수정, 삭제 등의 작업을 하게 만드는 공격 방법



- CSRF Token 적용

  - DTL csrf_token 태그를 사용해 사용자들에게 토큰 값을 부여
  - 요청 시 토큰 값도 함께 서버로 전송될 수 있도록 함

  ```html
  <!-- templates/articles/new.html -->
  
  <h1>NEW</h1>
  <form action = "{% url 'articles:create' %}" method="POST">
      {% csrf_token %}
      ...
  ```

  - 요청 시 CSRF Token을 함께 보내야 하는 이유
    - Django 서버는 해당 요청이 DB에 데이터를 하나 생성하는(DB에 영향을 주는)요청에 대해 "Django 가 직접 제공한 페이지에서 데이터를 작성하고 있는 것인지"에 대한 확인 수단이 필요한 것
    - 겉모습이 똑같은 위조 사이트나 정상적이지 않은 요청에 대한 방어 수단
    - 기존 : 요청 데이터 -> 게시글 작성
    - 변경 : 요청 데이터+인증 토큰 -> 게시글 작성

---

#### Delete

```python
# artucles/urls.py

urlpatterns = [
    ...
    path('<int:pk>/delete/', views/delete, name='delete'),
]
```

```python
# articles/views.py

def delete(request, pk):
    article = Article.objects.get(pk = pk)
    article.delete()
    return redirect('articles:index')
```

```html
<!-- articles/detail.html -->

<body>
    <h2>DETAIL</h2>
    ...
    <hr>
    <form action="{% url 'articles:delete' article.pk %}" method = "POST">
        {% csrf_token %}
        <input type="submit" value="DELETE">
    </form>
    <a href="{% url 'articles:index' %}">[back]</a>
</body>
```



---

#### Update

- 사용자가 입력 데이터를 받을 페이지를 렌더링 : edit
- 사용자가 입력한 데이터를 받아 DB에 저장 : update



- edit 기능 구현

  ```python
  # articles/urls.py
  
  urlpatterns = [
      ...
      path('<int:pk>/edit/', views.edit, name='edit'),
  ]
  ```

  ```python
  # articles/views.py
  
  def edit(request, pk):
      article = Article.object.get(pk=pk)
      context = {
          'article':article,
      }
      return render(request, 'articles/edit.html', context)
  ```

  ```html
  <!-- 수정 시 이전 데이터가 출력 될 수 있도록 작성하기 -->
  <!-- aritcles/edit.html-->
  
  <h1>EDIT</h1>
  <form action="#" method="POST">
    {% csrf_token %}
    <div>
      <label for="title">Title: </label>
      <input type="text" name="title" id = "title" value="{{ articles.title }}">
    </div>
    <div>
      <label for="content">Content: </label>
      <textarea name="content" id="content">{{article.content}}</textarea>
    </div>
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[back]</a>
  ```

  ```html
  <!-- edit 페이지로 이동하기 위한 하이퍼링크 작성 -->
  <!-- articles/detail.html -->
  
  <body>
    <a href="{% url 'articles:edit' article.pk %}">EDIT</a><br>
    <form action="{% url 'articles:delete' article.pk %}" method="POST">
      {% csrf_token %}
      <input type="subit" value="DELETE">
    </form>
    <a href="{% url 'articles:index' %}">[back]</a>
  </body>
  ```

  

- update 기능 구현

  ```python
  # articles/urls.py
  
  urlpatterns = [
      ...
      path('<int:pk>/update/', views.update, name='update'),
  ]
  ```

  ```python
  # articles/views.py
  
  def update(request, pk):
      article = Article.objects.get(pk=pk)
      article.title = request.POST.get('title')
      article.content = request.POST.get('content')
      article.save()
      return retirect('articles:detail', article.pk)
  ```

  ```html
  <!-- 작성 후 게시글 수정 테스트 -->
  <!-- articles/edit.html -->
  
  <h1>EDIT</h1>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    <div>
      <label for="title">Title: </label>
      <input type="text" name="title" id = "title" value="{{ articles.title }}">
    </div>
    <div>
      <label for="content">Content: </label>
      <textarea name="content" id="content">{{article.content}}</textarea>
    </div>
    <input type="submit">
  </form>
  <hr>
  <a href="{% url 'articles:index' %}">[back]</a>
  ```

  

---

- NoReverseMatch 에러

  url만 찾아서 디버깅하기
{% endraw %}