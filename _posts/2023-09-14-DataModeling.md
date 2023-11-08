---
title: Django Data Modeling
date: 2023-09-14 19:06:00 +09:00
categories: [Django]
tags:
  [
    django,
    data,
    modeling,
    ERD,
  ]
---

# Data Modeling

>  데이터베이스 시스템을 시각적으로 표현하는 프로레스
>
> : 데이터 유형, 데이터 간의 관계 및 분석 등을 통해 비즈니스 요구사항을 만들어 낼 수 있도록 도움 



- ERD(Entity-Relationship Diagram)

  다이어그램을 사용하여 데이터베이스의 Entity(개체)간 관계를 나타내는 방법



- 구성요소
  - 네모 : Entity(개체) : Table
  - 원 : Attribute(속성) : Field
  - 마름모 : Relation(관계) : PK, FK



- 작성 예시

  - Entity(개체)는 글, 회원 ,댓글

  - Attribute

    글에는 제목, 내용, 작성일 등

    회원에는 이름, 나이, 이메일 등

    댓글에는 내용, 수정일, 작성일 등

  - Relationship 정의

    글을 회원이 작성(관계)했고, 댓글을 회원이 작성(관계)했고, 댓글은 글에 소속(관계) 되어있음.



- Relationship 표현 방법

  - Cardinality(집합) : (1:1), (N:1), (N:M)

  - Optionality : 필수, 선택

  - 직선 : 각 회원은 글 하나만 쓸 수 있으며, 각 글의 저자는 한 명 뿐이다.

    3줄 : 각 글의 저자는 1명 뿐이지만, 각 회원은 글을 여러 개 쓸 수 있다.

    수직선과 동그라미 : 각 글에는 반드시 회원이 있지만, 회원은 글을 안쓸수도 있다.

    ![](https://github.com/SeoJunHa96.github.io\_posts\ERD-R.png)


    

  - https://freehoon.tistory.com/60 참고



---

#### 데이터 모델링의 중요성

- 데이터베이스 소프트웨어 개발 오류 감소
- 설계 및 생성 속도와 효율성 촉진
- 조직 전체에서 데이터 문서화 및 시스템 설계의 일관성 조성
- 데이터 엔지니어와 비즈니스 팀 간의 커뮤니케이션



- ERD 작성 사이트

  https://www.erdcloud.com/
