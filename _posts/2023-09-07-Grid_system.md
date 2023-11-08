---
title: Bootstrap Grid System
date: 2023-09-07 19:06:00 +09:00
categories: [HTML]
tags:
  [
    html,
    bootstrap,
    grid,

  ]
---

# Bootstrap Grid system


웹 페이지의 레이아웃을 조정하는 데 사용되는 '12'개의 컬럼으로 구성된 시스템

목적 : 반응 디자인을 지원해 웹 페이지를 다양한 기기에서 적절하게 표시할 수 있도록 도움



- Grid systen 기본 요소

  1. container : column들을 담고 있는 공간
  2. column : 실제 콘텐츠를 포함하는 부분
  3. gutter : 컬럼과 컬럼 사이의 여백 영역, x축은 padding, y축은 margin으로 여백 생성

  1개의 row 안에 12간의 column영역 구성, 각 요소는 12칸 중 몇 개를 차지할 것인지 지정됨

  ```html
  <div class="container">
      <div class="row">
          <div class="col-4"></div>
          <div class="col-4"></div>
          <div class="col-4"></div>
      </div>
  </div>
  <!-- 4칸씩 나눴음 -- >
  ```

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet"
      integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
    <style>
      .box {
        border: 1px solid black;
        background-color: lightblue;
        text-align: center;
      }
    </style>
  </head>
  <!-- basic-->
  <body>
    <h2 class="text-center">Basic</h2>
    <div class="container">
      <div class="row">
        <div class="box col-4">col</div>
        <div class="box col-4">col</div>
        <div class="box col-4">col</div>
      </div>
      <div class="row">
        <div class="box col-4">col-4</div>
        <div class="box">col-4</div>
        <div class="box">col-4</div>
      </div>
      <div class="row">
        <div class="box col-2">col-2</div>
        <div class="box col-8">col-8</div>
        <div class="box col-2">col-2</div>
      </div>
    </div>
  
    <hr>
  <!-- Nesting-->
    <h2 class="text-center">Nesting</h2>
    <div class="container">
      <div class="row">
        <div class="box col-4">col-4</div>
        <div class="box col-8">
          <div class="row">
            <div class="box col-6">col-6</div>
            <div class="box col-6">col-6</div>
            <div class="box col-6">col-6</div>
            <div class="box col-6">col-6</div>
          </div>
        </div>
      </div>
    </div>
  
    <hr>
  <!-- Offset(상쇄) -->
    <h2 class="text-center">Offset</h2>
    <div class="container">
      <div class="row">
        <div class="box col-4">col-4</div>
        <div class="box col-4 offset-4">col-4 offset-4</div>
      </div>
      <div class="row">
        <div class="box col-3 offset-3">col-3 offset-3</div>
        <div class="box col-3 offset-3">col-3 offset-3</div>
      </div>
      <div class="row">
        <div class="box col-6 offset-3">col-6 offset-3</div>
      </div>
    </div>
  
    <hr>
  
  <!-- Gutters 사이 여백 -->
    <h2 class="text-center">Gutters(gx-0)</h2>
    <div class="container">
      <div class="row gx-0">
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
      </div>
    </div>
  
    <br>
  
    <h2 class="text-center">Gutters(gy-5)</h2>
    <div class="container">
      <div class="row gy-5">
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
      </div>
    </div>
  
  
    <br>
  
    <h2 class="text-center">Gutters(g-5)</h2>
    <div class="container">
      <div class="row g-5">
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
        <div class="col-6">
          <div class="box">col</div>
        </div>
      </div>
    </div>
  
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
      crossorigin="anonymous"></script>
  </body>
  
  </html>
  
  ```

  

- Nesting

  하나의 row안에서 또 하나의 row를 만드는 것

  즉, 12개의 그리드 안에 다시 12개의 그리드로 나눠서 배치하는 것.

---

####  Resposive Web Design

반응형 웹 디자인

Bootstrap gird system에서는 12개 column과 6개 breakpoints를 사용하여 반응형 웹 디자인을 구현



- Grid system breakpoints

  웹 페이지를 다양한 화면 크기에서 적절하게 배치하기 위한 분기점

  화면 '너비'에 따라 6개의 분기점 제공(xs(576미만), sm(576이상), md(768이상), lg(992이상), xl(1200이상), xxl(1400이상))

  각 breakpoint마다 설정된 최대 너비값 '이상으로' 화면이 커지면 gird system 동작이 변경됨

  

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  <style>
    .box {
      border: 1px solid black;
      background-color: lightblue;
      text-align: center;
    }
  </style>
</head>

<body>
  <h2 class="text-center">Breakpoints</h2>
  <div class="container">
    <div class="row">
      <div class="col-12 col-sm-6 col-md-2 col-lg-3 col-xl-4 box">
        col
      </div>
      <div class="col-12 col-sm-6 col-md-8 col-lg-3 col-xl-4 box">
        col
      </div>
      <div class="col-12 col-sm-6 col-md-2 col-lg-3 col-xl-4 box">
        col
      </div>
      <div class="col-12 col-sm-6 col-md-12 col-lg-3 col-xl-12  box">
        col
      </div>
    </div>

    <hr>

    <h2 class="text-center">Breakpoints + offset</h2>
    <div class="row g-4">
      <div class="col-12 col-sm-4 col-md-6 box">
        col
      </div>
      <div class="col-12 col-sm-4 col-md-6 box">
        col
      </div>
      <div class="col-12 col-sm-4 col-md-6 box">
        col
      </div>
      <div class="col-12 col-sm-4 col-md-6 offset-sm-4 offset-md-0 box">
        col
      </div>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
    crossorigin="anonymous"></script>
</body>

</html>

```



- Media Query로 작성된 Grid system의 breakpoint

  ```html
  @media(min-width: 576px){
  
  }
  @media(min-width: 768px){
  
  }
  @media(min-width: 992px){
  
  }
  @media(min-width: 1200px){
  
  }
  @media(min-width: 1400px){
  
  }
  ```



- Grid cards

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet"
      integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
  </head>
  
  <body>
    <h2 class="text-center">Grid Cards</h2>
    <div class="container">
      <div class="row row-cols-1 row-cols-sm-3 row-cols-md-2 g-4">
        <div class="col">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional
                content. This content is a little bit longer.</p>
            </div>
          </div>
        </div>
        <div class="col">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional
                content. This content is a little bit longer.</p>
            </div>
          </div>
        </div>
        <div class="col">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional
                content.</p>
            </div>
          </div>
        </div>
        <div class="col offset-sm-4 offset-md-0">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional
                content. This content is a little bit longer.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"
      crossorigin="anonymous"></script>
  </body>
  
  </html>
  
  ```

  

