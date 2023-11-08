---
title: Django Model
date: 2023-09-14 19:06:00 +09:00
categories: [Django]
tags:
  [
    django,
    model,
    crud,
  ]
---

# Django Model

#### Model

Model을 통한 DB(데이터베이스) 관리

- Django Model

  DB의 "테이블을 정의"하고 "데이터를 조작"할 수 있는 기능들을 제공하여 "테이블 구조를 설계"하는 청사진



- model 클래스 작성

  ```python
  # articles/models.py
  
  class Article(models.Model):
      title = models.CharFiedl(max_length=10) #제목 최대길이를 10으로 제한
      content = models.TextField()
      
  # 테이블 설계도, id필드는 Django가 자동 생성
  ```

  ```python
  class Article(models.Model): # Model은 model에 관련된 모든 코드가 이미 작성 되어있는 클래스
      title = models.CharFiedl(max_length=10)
      content = models.TextField()
  # title, content는 테이블의 각 필드(열)이름, 클래스 변수명
  # CharField, TextField는 model Field 클래스, 테이블 필드의 데이터 타입.
  # 모델 필드 클래스의 키워드 인자는 필드 옵션으로 테이블 필드의 제약 조건
  ```

  - 제약 조건 : 데이터가 올바르게 저장되고 관리되도록 하기 위한 규칙

---

#### Migrations (가장 중요)

model 클래스의 변경사항(필드 생성, 수정, 삭제 등)을 DB에 최종 반영하는 방법

- Migrations 과정 (순서, 명령어 중요)

  ```python
  1. model class # 설계도 초안
  
  2. python manage.py makemigrations  # 명령어 중요
  
  3. migration 파일(최종 설계도) 생성
  
  4. python manage.py migrate # 명령어 중요, 데이터 베이스에 반영
  
  5. db.sqlite3(DB)
  ```

  - articles/models.py에서 model클래스를 활용해서 설계도 초안을 만든다.
  - makemigrations를 사용해서 최종 설계도(migration)를 작성한다.
  - 0001_initial.py와 같은 파일 생성 확인
  - migrate명령어를 통해 최종 설계도를 DB에 전달하여 반영한다.
  - mitrate 후 DB내에 생성된 테이블을 확인



- 추가 Migrations

  이미 생성된 테이블에 필드 추가

  1. articles/models.py 파일에 추가 모델 필드 작성

  2. 이미 기존 테이블이 존재하기 때문에 필드를 추가 할 때 필드의 기본 값 설정이 필요하다.

     - 현재 대화를 유지하면서 직접 기본 값을 입력 하는 방법
     - 현재 대화에서 나간 후 models.py에 기본 값 관련 설정을 하는 방법

  3. python manage.py makemigrations

  4. 추가하는 필드의 기본값을 입력하는 상황에는 Django가 제안하는 기본 값을 사용하는 것을 권장

  5. migrations 과정 종료 후 2번째 migration 파일이 생성된 것을 확인

     (설계도를 쌓아가면서 추후 문제가 생겼을 시 복구를 위해)

  6. python magage.py migrate 후 테이블 필드 변화 확인



- model class에 변경사항이 생겼다면(1), 반드시 새로운 설계도를 생성하고(2), 이를 DB에 반영한다.(3)

  1. model class 변경

  2. makemigrations

  3. migrate

     

---

#### Model Field

DB 테이블의 필드(열)을 정의하며, 해당 필드에 저장되는 데이터 타입과 제약조건을 정의

- CharField() : 길이의 제한이 있는 문자열을 넣을 때 사용(max_length는 필수 인자)

- TextField() : 글자 수가 많을 때 사용

- DateTimeField() : 날짜와 시간을 넣을 때 사용

  - datetimefield의 선택인자

  - auto_now : 데이터가 저장될 때마다 자동으로 현재 날짜시간 저장(수정시 사용)
  - auto_now_add : 처음 생성될 때만 저장



---

#### Admin site

Automatic admin interface

Django는 추가 설치 및 설정 없이 자동으로 관리자 인터페이스를 제공, 데이터 확인 및 테스트 등을 진행하는데 유용



- admin 계정 생성(email은 선택사항)

  python manage.py createsuperuser

- 생성된 계정은 데이터베이스 auth_user에 저장된다.

- admin에 모델 클래스 등록

  admin.py에 작성한 모델 클래스를 등록해야만 admin site에서 확인 가능

  ```python
  # articles/admin.py
  
  from django.contrib import admin
  from .models import Article
  
  admin.site.register(Article)
  ```

  

---

#### 데이터베이스 초기화

- Migrataion 파일 삭제
- db.sqlite.3 파일 삭제
- init.py파일, migrations폴더 삭제 하지 않도록 주의



- 기타 명령어

  ```python
  # migrations파일들이 migrate 됐는지 여부를 확인, [X]표시는 완료
  python manage.py showmigrations
  
  # 해당 migrations파일이 SQL언어로 어떻게 번역되어 DB에 전달되는지 확인하는 명령어
  python manage.py sqlmigrate atricles 0001
  
  ```

  

---

#### CRUD

create, read, update, delete

소프트웨어가 가지는 기본적인 데이터 처리 기능은 저장, 조회, 갱신, 삭제의 틀에서 크게 벗어나지 않는다.



---

- urls.py를 통해 app을 연결한다.
- app은 하나의 project
- app 안에는 views.py, models.py, templates 등이 존재하며
- views.py를 통해 필요한 models나 templates를 연결
- 이 중 models는 database와 관련

---

### 중요 명령어

1. python manage.py showmigrations

   상태 확인 (git으로 따지면 git status)

2. python manage.py makemigrations

3. python manage.py migrate

   반영

4. python manage.py sqlmitrate articles 0001

   어떻게 sql 언어로 번역되어 DB에 전달되었는지 확인