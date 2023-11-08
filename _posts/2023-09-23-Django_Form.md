---
title: Django Form
date: 2023-09-26 19:06:00 +09:00
categories: [Django]
tags:
  [
    django,
    form,
    meta,
    
  ]
---

# Django Form
{% raw %}

#### HTML Form

- HTML 'form'

  지금까지 사용자로부터 데이터를 받기 위해 활용한 방법

  그러나 비정상적 혹은 악의적인 요청을 필터링 할 수 없음

  : 유효한 데이터인지에 대한 확인이 필요



- 유효성 검사

  수집한 데이터가 정확하고 유효한지 확인하는 과정



- 유효성 검사 구현

  유효성 검사를 구현하기 위해서는 입력 값, 형식, 중복, 범위, 보안 등 고려

  이런 과정과 기능을 직접 개발하는 것이 아닌 Django가 제공하는 Form을 사용



---

#### Form Class

- Django Form

  사용자 입력 데이터를 수집, 처리 및 유효성 검사를 수행하기 위한 도구

  : 유효성 검사를 단순화하고 자동화 할 수 있는 기능을 제공

  

- Form class 정의

  ```python
  # articles/forms.py
  
  from Django import forms
  
  class ArticleForm(forms.Form):
      title = forms.CharField(max_length=10)
      content = forms.CharField()
  ```

  

- Form class를 적용한 new 로직

  ```python
  # articles/views.py
  
  from .forms import ArticleForm
  
  def new(request):
      form = ArticleForm()
      context = {
          'form':form,
      }
      return render(request, 'articles/new.html', context)
  ```

  ```html
  <!-- articles/new.html -->
  
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
      {% csrf token %}
      {{ form }}
      <input type="submit">
  </form>
  ```

  

- Form rendering option

  label, input 쌍을 특정 HTML 태그로 감싸는 옵션

  ```html
  <!-- articles/new.html -->
  <!-- form.as_p-->
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" methode="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  ```

  

---

#### Widgets

- HTML 'input' element의 표현을 담당



- Widget은 단순히 input 요소의 속성 및 출력되는 부분을 변경하는 것

  ```python
  # articles/form.py
  
  from django import forms
  
  class ArticleForm(forms.Form):
      title = forms.CharField(max_length = 10)
      content = forms.CharField(widget-forms.textarea)
  ```



---

#### Django ModelForm



- Form : 사용자 입력 데이터를 DB에 저장하지 않을 때(로그인 처럼)
- ModelForm : 사용자 입력 데이터를 DB에 저장해야 할 때(게시글, 회원가입)



- ModelForm 

  Model과 연결된 Form을 자동으로 생성해주는 기능을 제공

  Form + Model



- ModelForm class 정의

  기존 ArticleForm 클래스 수정

  ```python
  # articles/forms.py
  
  from django import forms
  from .models import Article
  
  class ArticleForm(forms.ModelForm):
      class Meta:
          model = Article
          fields = '__all__'
  ```

  

- Meta class

  Model Form의 정보를 작성하는 곳

  - fields 및 exclude 속성

    exclude 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 수도 있음

    ```python
    # articles/forms.py
    
    class ArticleForm(forms.ModelForm):
        class Meta:
            model = Article
            fields = ('title',)
    ```

    ```python
    # articles/forms.py
    
    class ArticleForm(forms.ModelForm):
        class Meta:
            model = Article
            exclude = ('title',)
    ```

  - ModelForm을 적용한 create로직

    ```python
    # articles/views.py
    from .forms import ArticleForm
    
    def create(request):
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
        context = {
            'form':form,
        }
        return render(request, 'articles/new.html', context)
    ```

    - is_valid

      여러 유효성 검사를 실행했고, 데이터가 유효한지 여부를 bool값으로 반환

      빈값을 허용하지 않음



- ModelForm을 적용한 edit 로직

  ```python
  # articles/views.py
  
  def edit(request, pk):
      article = Article.objects.get(pk=pk)
      form = ArticleForm(instance=article)
      context = {
          'article':article,
          'form': form,
      }
      return render(request, 'articles/edit.html', context)
  ```

  ```html
  <!-- articles/edit.html -->
  <<h1>EDIT</h1>
  <form action="{% url 'articles:update' article.pk %}" methode="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
  ```

  ```python
  # articles/views.py
  
  def update(request, pk):
      article = Article.objects.get(pk=pk)
      form = ArticleForm(request.POST, instance = article)
      if form.is_valid():
          form.save()
          return redirect('articles:detail', article.pk)
      context = {
          'form':form,
      }
      return render(request, 'articles/edit.html', context)
  ```

  

- Django Form 정리

  사용자로부터 데이터를 수집하고 처리하기 위한 도구

  HTML form의 생성, 데이터 유효성 검사 및 처리를 쉽게 할 수 있도록 도움



- Widget 응용

  ```python
  # articles/forms.py
  
  class ArticleForm(forms.ModelForm):
      title = forms.CharField(
      	label = '제목',
      	widget = form.TextInput(
          	attrs={
                  'class' : 'my-title',
                  'placeholder' : 'Enter the title',
              }
          )
      )
      class Meta:
          model = Article
          fields = '__all__'
  ```

  ```python
  class ArticleForm(forms.ModelForm):
      title = forms.CharField(
      	label = '제목',
      	widget = form.TextInput(
          	attrs={
                  'class' : 'my-title',
                  'placeholder' : 'Enter the title',
                  'maxlength' : 10
              }
          )
      )
      content = forms.CharField(
      	label = '내용',
      	widget = forms.Textarea(
          	attrs={
                  'class': 'my-content',
                  'placeholder' : 'Enter the content',
                  'rows' : 5,
                  'cols' : 50,
              }
          ),
          error_messages={'required': '내용을 입력해주세요.'},
      )
      ...
  ```



---

#### Handling Http requests



- view 함수 구조 변화
  - new 와 create view 함수는 "데이터 생성을 구현"하기 위한다는 공통의 목적을 가짐
  - 단, new는 GET method, create는 POST method 요청만을 처리한다.

```python
def new(request):
    form = ArticleForm()
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)

def create(request):
    form = ArticleForm(request.POST)
    if form.is_valid():
        article = form.save()
        return redirect('articles:detail', article.pk)
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)
```

```python
# new & create 함수 결합

def create(request):
    # request method에 따른 분기
    if request.method == 'POST':
        # POST일 때는 과거 create함수 구조였던 객체 생성 및 저장 로직 처리
        form = ArticleForm(request.POST)
        if form.is_vaild():
            article = form.save()
            return redirect('articles:detail', article.pk)
    else:
        # POST가 아닐 때는 과거 단순히 form 인스턴스 생성
        form = ArticleForm()
    # context에 담기는 form은
    # 1. is_valid를 통과하지 못해 에러메시지를 담은 form이거나
    # 2. else문을 통한 form 인스턴스
    context = {
        'form':form,
    }
    return render(request, 'articles/new.html', context)
```



- 기존 new 관련 코드 수정

  - 사용하지 않는 new url 제거

  - new url을 create url로 변경

    ```html
    <!-- articles/index.html -->
    
    <a herf="{% url 'articles:create' %}">CREATE</a>
    ```

    ```html
    <!-- articles/create.html -->
    
    <form action="{% url 'articles:create' %}" method="POST">
        ...
    </form>
    ```

  - new 템플릿을 create 템플릿으로 변경

    ```python
    def create(request):
        ...
        return render(request, 'articles/create.html', context)
    ```



- request method에 따른 요청의 변화
  - GET : 게시글 생성 문서 요청
  - POST : 게시글 생성 요청



- 기존 edit과 update view 함수 결합

  ```python
  # articles/views.py
  
  def update(request, pk):
      article = Article.objects.get(pk=pk)
      # update 기능
      if request.method == 'POST':
          form = ArticleForm(request.POST, instance=article)
          if form.is_valid():
              form.save()
              return redirect('articles:detail', article.pk)
          else:
              # edit 기능
              form = ArticleForm(instance=article)
          context = {
              'article' : article,
              'form': form,
          }
          return render(request, 'artcies/update.html', context)
  ```

  - 사용하지 않는 edit url 제거

  - 기존 edit 관련 코드 수정(edit 템플릿을 update 템플릿으로 변경)

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
    <a href="{% url'articles:update' article.pk %}">UPDATE</a>
    ```
{% endraw %}
    



---

코드 자체를 외우려 하기보다는 구조/틀을 이해해야 한다.