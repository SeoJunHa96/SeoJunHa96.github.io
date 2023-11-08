---
title: Bootstrap
date: 2023-09-06 19:06:00 +09:00
categories: [HTML]
tags:
  [
    html,
    bootstrap,
  ]
---

# Bootstrap

#### Bootstrap 이란?

CSS 프론트엔드 프레임워크(Toolkit)

미리 만들어진 다양한 디자인 요소들을 제공하여 웹 사이트를 빠르고 쉽게 개발할 수 있도록 함.



- 적용 방법

  ```html
  <!--헤드 태그 종료 직전 -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
  
  <!-- 바디 태그 닫히기 직전 -->
   <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
  ```

  - reset css

    브라우저 마다 초기 설정이 다르기 때문에 부트 스트랩을 입히면 모든 설정이 초기화된다.

    : 어떤 브라우저에서 열어도 시작점을 똑같이 만들고 시작한다.



- Bootstrap 기본 사용법

  ```html
  <p class="mt-5">Hello, world!</p>
  {property}(m){sides}(t)-{size}(5)
  <!-- 마진 탑 - 5 -->
  ```



- property

  m : margin

  p : padding



- sides

  t : top

  b : bottom

  s : left

  e : right

  y : top, bottom

  x : left, right

  blank : 4sides



- size

  0 : 0 rem, 0px

  1 : 0.25 rem, 4px

  2 : 0.5 rem, 8px

  3 : 1 rem, 16px

  4 : 1.5 rem, 24px

  5 : 3  rem, 48px

  (이 이상은 커스텀 해야함)

  auto : auto



- Bootstrap에는 특정한 규칙이 있는 클래스 이름으로 이미 스타일 및 레이아웃이 작성되어 있음



---

#### Typography

제목, 본문 텍스트, 목록 등

- 종류

  - Display heading (class="display-1~6")

  - Inline text elements

  - Lists

    등

---

#### Colors

Bootstrap이 지정하고 제공하는 색상 시스템



---

#### Component

Bootstrap에서 제공하는 UI관련 요소 (버튼, 네비게이션 바, 카드, 폼, 드롭다운 등)

일관된 디자인을 제공하여 웹사이트의 구성 요소를 구축하는데 유용하게 활용

- 대표 컴포넌트
  - Alerts(경고창)
  - Badges(알림창?, 예를 들어 카톡이 왔을 때 생기는 빨간 점?)
  - Buttons(버튼)
  - Cards
  - Navbar
  - carousel(눌렀을 때 화면 넘어가는 기능)

---

 #### Semantic Web

웹 데이터를 의미론적으로 구조화된 형태로 표현하는 방식

- \<h1>Heading\</h1>

  페이지 최상위 제목 '의미'를 제공하는 semantic 요소

  브라우저에 의해 제목처럼 보이도록 스타일이 지정됨

- Html Semantic Element

  기본적인 모양과 기능 이외에 의미를 가지는 HTML요소

  검색엔진 및 개발자가 웹 페이지 콘텐츠를 이해하기 쉽도록 한다.

  - 종류

    header(최상위), nav(네비게이션), main(중심 내용 박스), article, section, aside, footer(바닥글)



- Semantic in CSS

  - OOCSS(Object Oriented CSS)

    객체 지향적 접근법을 적용하여 CSS를 구성하는 방법론

    CSS를 효율적이고 유지 보수가 용이하게 작성하기 위한 일련의 가이드라인

    1. 구조와 스킨을 분리

       구조와 스킨을 분리함으로써 재사용 가능성을 높임

       모든 버튼의 공통 구조를 정의, 각각의 스킨을 정의

    2. 커네이너와 콘텐츠를 분리

       객체에 직접 적용하는 대신 객체를 둘러싸는 컨테이너에 스타일 적용

       스타일을 정의할 때 위치에 의존하는 스타일을 사용하지 않도록 함

       콘텐츠를 다른 컨테이너로 이동시키거나 재배치할 때 스타일이 깨지는 것을 방지

       

---

- 파란색 박스 만들기

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
    <style>
        <!-- 박스 크기 -->
      .box{
        height: 200px;
        width: 200px;
      }
    </style>
  </head>
  
  <body>
      <!-- 박스 속성(크기), 테두리, 테두리 색, 배경색-->
    <div class="box border border-dark bg-info"></div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
  </body>
  
  </html>
  
  ```

  

---

- CDN

  지리적 제약 없이 빠르고 안전하게 콘텐츠를 전송할 수 있는 전송 기술

  서버와 사용자 사이의 물리적인 거리를 줄여 콘텐츠 로딩에 소요되는 시간을 최소화.





---

- HTML은 콘텐츠의 구조와 의미, 디자인을 바꾸기 위해서 구조를 바꿔서는 안됨

- CSS는 레이아웃과 디자인. 배치.

- 이론적인 부분은 만들 때 보다는 고칠 때 의미가 있을 것.

  

---

#### CSS 미디어 쿼리(Media Query)

- 기본 문법

  if 조건문과 비슷한 개념

  ```html
  @media(조건) {
  	스타일(css코드)
  }
  ```

  조건 부분이 만족될 때는 스타일이 적용, 만족되지 않을 때는 스타일 무시.



- 좁은 화면 스타일링

  좁은 화면에서만 특정 스타일을 적요하고 싶을 때

  ```html
  @media(max-with: 800px){
  	.small-tomato{
  		background-color: tomato;
  	}
  }
  ```

  800px 이하의 좁은 화면에서 특정 Html 요소의 배경색을 토마토 색으로 바꾸는 것.



- 넓은 화면 스타일링

  800px 이상의 넓은 화면에서

  ```html
  @media (min-width: 800px){
  	.large-tomato{
  		color: tomato;
  	}
  }
  ```

  

- 화면 너비에 따라 Html요소 숨기기

  목록에서 어떤 항목은 넓은 화면에서 숨기고 어떤 항목은 좁은 화면에서 숨길때

  ```html
  @media(max-width: 600px) {
  	.desktop{
  		display: none;
  	}
  }
  @media(min-width: 1000px) {
  	.desktop{
  		display: none;
  	}
  }
  ```

  