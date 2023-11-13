---
title: Vue Basic Syntax 2
date: 2023-11-06 19:06:00 +09:00
categories: [Vue]
tags:
  [
    vue,
    computed,
    v-if,
    v-show,
    v-for,
    watch,
  ]
---

#  Vue Basic Syntax 2

{% raw %}
#### Computed Properties

- computed() : 계산된 속성을 정의하는 함수

  미리 계산된 속성을 사용하여 템플릿에서 표현식을 단순하게 하고 불필요한 반복 연산을 줄임

```html
<body>
  <div id="app">
    <h2>남은 할 일</h2>
    <p>{{ restOfTodos }}</p>
    <p>{{ getRestOfTodos() }}</p>
</div>

<script>
  const { createApp, ref, computed } = Vue

  const restOfTodos = computed(() => {
    return todos.value.length > 0 ? '아직 남았다' : '퇴근!'
  })
</script>
```

반응성 데이터를 포함하는 복잡한 로직의 경우 computed를 활용하여 미리 값을 계산



- computed 특징

  반환되는 값은 computed ref이며 일반 refs와 유사하게 계산된 결과를 .value로 참조할 수 있음(템플릿에서는 .value 생략 가능)

  computed 속성은 의존된 반응형 데이터를 자동으로 추적

  의존하는 데이터가 변경될 때만 재평가

  ```js
  const restOfTodos = computed(() => {
      return todos.value.length > 0? '아직 남았다' : '퇴근!'
  })
  // restOfTodos의 계산은 todos에 의존하고 있음
  // 따라서 todos가 변경될 때만 restOfTodos가 업데이트 됨
  ```



- method

  computed 속성 대신 method로도 동일한 기능을 정의할 수 있음

  두 가지 접근 방식은 실제로 완전히 동일

  ```html
  <p>{{ getRestOfTodos() }}</p>
  <script>
  const getRestOfTodos = function () {
    return todos.value.length > 0 ? '아직 남았다' : '퇴근!'
  }
  </script>
  ```



- computed와 method 차이
  - computed 속성은 의존된 반응형 데이터를 기반으로 캐시(cached)된다.
  - 의존하는 데이터가 변경된 경우에만 재평가됨
  - 즉, 의존된 반응형 데이터가 변경되지 않는 한 이미 계산된 결과에 대한 여러 참조는 다시 평가할 필요 없이 이전에 계산된 결과를 즉시 반환
  - 반면, method 호출은 다시 렌더링이 발생할 때마다 항상 함수를 실행한다.



- Cache(캐시)

  데이터나 결과를 일시적으로 저장

  이후에 같은 데이터나 결과를 다시 계산하지 않고 빠르게 접근



- 적절한 사용처

  - computed

    의존하는 데이터에 따라 결과가 바뀌는 계산된 속성을 만들 때

    동일한 의존성을 가진 여러 곳에서 사용할 때 계산 결과를 캐싱하여 중복 계산 방지

  

  - method

    단순히 특정 동작을 수행하는 함수를 정의할 때 사용

    데이터에 의존하는지 여부와 관게 없이 항상 동일한 결과를 반환하는 함수



- 정리

  computed : 의존된 데이터가 변경되면 자동 업데이트

  method : 호출해야 실행

  사용 목적과 상황에 맞게 적절히 조합하여 사용



---

#### Conditional Rendering



- 표현식 값의 T/F를 기반으로 요소를 조건부로 "렌더링"

  ```html
  <!-- if else -->
  <p v-if="isSeen">true일때 보여요</p>
  <p v-else>false일때 보여요</p>
  <button @click="isSeen = !isSeen">토글</button>
  
  const isSeen = ref(true)
  ```

  ```html
  <div v-if="name === 'Alice'">Alice입니다</div>
  <div v-else-if="name === 'Bella'">Bella입니다</div>
  <div v-else-if="name === 'Cathy'">Cathy입니다</div>
  <div v-else>아무도 아닙니다.</div>
  
  const name = ref('Cathy')
  ```

  

  - 여러 요소에 대한 v-if 적용

    v-if는 directive이기 때문에 단일 요소에만 연결 가능

    이 경우 template 요소에 v-if를 사용하여 하나 이상의 요소에 대해 적용할 수 있음(v-else, v-else-if 모두 적용 가능)

    ```html
    <!-- v-if on <template> -->
    <template v-if="name === 'Cathy'">
      <div>Cathy입니다</div>
      <div>나이는 30살입니다</div>
    </template>
    ```

    

- HTML \<template> element

  페이지가 로드 될 때 렌더링 되지 않지만 JS를 사용하여 나중에 문서에서 사용할 수 있도록 하는 HTML을 보유하기 위한 메커니즘

  "보이지 않는 wrapper 역할 "



- v-show

  표현식 값의 T/F를 기반으로 요소의 가시성을 전환(가시성과 렌더링을 혼동하지 말 것!)

  v -show 요소는 항상 렌더링 되어 DOM에 남아 있음

  CSS display 속성만 전환하기 때문

  ```html
  <div v-show="isShow">v-show</div>
  
  const isShow = ref(false)
  ```

  ```html
  <div style="display:none;">v-show</div>
  ```

  

- v-if 와 v-show

  - v-if (Cheap initial load, expensive toggle)

    초기 조건이 false인 경우 아무 작업도 수행하지 않음

    토글 비용이 높음 (빈번한 토글 작업이 필요하고 각각의 토글 작업이 실행되면 많은 시간 또는 컴퓨팅 자원이 소모)

  

  - v-show

    초기 조건에 관계 없이 항상 렌더링

    초기 렌더링 비용이 더 높음

  

  > 자주 전환해야 하는 경우에는 v-show를, 실행 중 조건이 변경되지 않는 경우에는 v-if를 권장



---

#### List Rendering



- v-for

  소스 데이터(Array, Object, Number, String, Iterable)를 기반으로 요소 또는 템플릿 블록을 여러 번 렌더링



- v-for 구조

  - alias in expression 형식의 특수 구문을 사용하여 반복되는 현재 요소에 대한 별칭(alias)을 제공

  ```html
  <div v-for="item in items">
      {{ item.text }}
  </div>
  ```

  

  - 인덱스(객체에서는 키)에 대한 별칭을 지정할 수 있음

  ```html
  <div v-for="(item, index) in items>"</div>
  
  <div v-for="value in object>"</div>
  <div v-for="(value, key) in object>"</div>
  <div v-for="(value, key, index) in object>"</div>
  ```

  value, key, index 순서는 정해져있음.(바꾸면 안됨)

  

  - 배열 반복

  ```html
  <div v-for="(item, index) in myArr">
    {{ index }} // {{ item.name }}
  </div>
  
  const myArr = ref([
    { name: 'Alice', age: 20 },
    { name: 'Bella', age: 21 }
  ])
  ```

  

  - 객체 반복

  ```html
  <div v-for="(value, key, index) in myObj">
    {{ index }} / {{ key }} / {{ value }}
  </div>
  
  const myObj = ref({
    name: 'Cathy',
    age: 30
  })
  ```

  

- 여러 요소에 대한 v-for 적용

  template 요소에  v-for를 사용하여 하나 이상의 요소에 대해 반복 렌더링 할 수 있음

  ```html
  <!-- v-for on <template> -->
  <ul>
    <template v-for="item in myArr">
      <li>{{ item.name }}</li>
      <li>{{ item.age }}</li>
      <hr>
    </template>
  </ul>
  ```

  

- 중첩된 v-for

  ```html
  <!-- nested v-for -->
  <ul v-for="item in myInfo">
    <li v-for="friend in item.friends">
      {{ item.name }} - {{ friend }}
    </li>
  </ul>
  
  // nested v-for
  const myInfo = ref([
    { name: 'Alice', age: 20, friends: ['Bella', 'Cathy', 'Dan'] },
    { name: 'Bella', age: 21, friends: ['Alice', 'Cathy'] }
  ])
  ```

  

- v-for with key

  내부 컴포넌트의 상태를 일관되게 유지
  데이터의 예측 가능한 행동을 유지 (Vue 내부 동작 관련)

  > 반드시 v-for와 key를 함께 사용한다.

  - key는 반드시 각 요소에 대한 고유한 값을 나타낼 수 있는 식별자여야 함.

  ```html
  <div v-for="item in items" :key="item.id">
    <!-- content -->
    {{ item }}
  </div>
      
  const items = ref([
    { id: id++, name: 'Alice' },
    { id: id++, name: 'Bella' },
  ])
  ```

  

- 동일 요소에 v-for와 v-if를 함께 사용하지 않는다.

  동일한 요소에서 v-if가 v-for보다 우선순위가 더 높기 때무

  > v-if 조건은 v-for범위의 변수에 접근할 수 없음



- todo 데이터 중 이미 처리한 (isComplete === true) todo만 출력하기

  ```html
  <ul>
    <li v-for="todo in completeTodos" :key="todo.id">
      {{ todo.name }}
    </li>
  </ul>
  
  const completeTodos = computed(() => {
    return todos.value.filter((todo) => !todo.isComplete)
  })
  ```

  

- v-for의 todo요소를 v-if에서 사용할 수 없음 : v-for와 template요소를 사용하여 v-if를 이동

  ```html
  <ul>
    <template v-for="todo in todos" :key="todo.id">
      <li v-if="!todo.isComplete">
        {{ todo.name }}
      </li>
    </template>
  </ul>
  ```

  

---

#### Watchers



- watch()

  반응형 데이터를 감시하고, 감시하는 데이터가 변경되면 콜백 함수를 호출



- watch 구조

  ```js
  watch(varaiable, (newValue, oldValue) => {
      // do something
  })
  ```

  - variable : 감시하는 함수
  - newValue : 감시하는 변수가 변화된 값, 콜백 함수의 첫 번째 인자.
  - oldValue : 콜백 함수의 두 번째 인자



- watch 예시

  1. 감시하는 변수에 변화가 생겼을 때 기본 동작 확인하기

  ```html
  <button @click="count++">Add 1</button>
  <p>Count: {{ count }}</p>
  
  const count = ref(0)
  const countWatch = watch(count, (newValue, oldValue) => {
    console.log(`newValue: ${newValue}, old Value: ${oldValue}`)
  })
  ```

  

  2. 감시하는 변수에 변화가 생겼을 때 연관 데이터 업데이트 하기

  ```html
  <input v-model="message">
  <p>Message length: {{ messageLength }}</p>
  
  const messageWatch = watch(message, (newValue, oldValue) => {
    messageLength.value = newValue.length
  })
  ```

  

- Computed와 Watchers

  |           |                computed                 |                      watchers                       |
  | --------- | :-------------------------------------: | :-------------------------------------------------: |
  | 공통점    |      데이터의 변화를 감지하고 처리      |            데이터의 변화를 감지하고 처리            |
  | 동작      | 의존하는 데이터 속성의 계산된 값을 반환 | 특정 데이터 속성의 변화를 감시하고<br />작업을 수행 |
  | 사용 목적 |  템플릿 내에서 사용되는 데이터 연산용   |         데이터 변경에 따른 특정 작업 처리용         |
  | 사용 예시 |  연산 된 길이, 필터링 된 목록 계산 등   |       비동기 API요청, 연관 데이터 업데이트 등       |

  - computed와 watch 모두 의존(감시)하는 원본 데이터를 직접 변경하지 않음

  

---

#### Lifecycle Hooks

Vue 인스턴스의 생애주기 동안 특정 시점에 실행되는 함수

> 개발자가 특정 단계에서 의도하는 로직이 실행될 수 있도록 함



- Lifecycle Hooks 예시

  1. vue 컴포넌트 인스턴스가 초기 렌더링 및 DOM 요소 생성이 완료된 후 특정 로직 수행하기

     ```js
     const { createApp, ref, onMounted, onUpdated } = Vue
     
     onMounted(() => {
       console.log('mounted')
     })
     ```

  

  2. 반응형 데이터의 변경으로 인해 컴포넌트의 DOM이 업데이트된 후, 특정 로직을 수행하기

     ```html
     <button @click="count++">Add 1</button>
     <p>Count: {{ count }}</p>
     <p>{{ message }}</p>
     
     const { createApp, ref, onMounted, onUpdated } = Vue
     
     const count = ref(0)
     const message = ref(null)
     
     onUpdated(() => {
       message.value = 'updated~!'
     })
     ```



- 특징
  - Vue는 Lifecycle Hooks에 등록된 콜백 함수들을 인스턴스와 자동으로 연결
  - 이렇게 동작하려면 hooks 함수들은 반드시 동기적으로 작성되어야 함
  - 인스턴스 생애 주기의 여러 단계에서 호출되는 다른 hooks도 있다.
  - 가장 일반적으로 사용되는 것은 onMounted, onUpdated, onUnmounted



- Lifecycle Hooks Diagram

  ```
  https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram
  ```



---

#### Vue Style Guide



- Vue의 스타일 가이드 규칙은 우선순위에 따라 4가지 범주로 나눔

  1. 우선순위 A : 필수(Essential)

     오류를 방지하는 데 도움이 되므로, 어떤 경우에도 규칙을 학습하고 준수

     (v-for에 key 작성하기, 동일 요소에 v-if와 v-for 함께 사용하지 않기 등)
     

  2. 우선순위 B : 적극 권장(Strongly Recommended)

     가독성 및 개발자 경험 향상

     규칙을 어겨도 코드는 여전히 실행되겠지만, 정당한 사유가 있어야 규칙을 위반할 수 있음

     

  3. 우선순위 C : 권장 (Recommended)

     일관성 보장하도록 임의의 선택을 할 수 있음
     

  4. 우선순위 D : 주의 필요 (Use with Caution)

     잠재적 위험 특성을 고려함

     

  ```
  https://vuejs.org/style-guide/
  ```

  

---

#### 주의사항

-  computed의 반환 값은 변경하지 말 것
  - computed의 반환 값은 의존하는 데이터의 파생된 값
  - 일종의 snapshot이며 의존하는 데이터가 변경될 때마다 새 snapshot이 생성됨
  - snapshot을 변경하는 것은 의미가 없으므로 계산된 반환 값은 읽기 전용으로 취급되어야 하며 변경되어서는 안됨
  - 대신 새 값을 얻기 위해서는 의존하는 데이터를 업데이트 해야 함



- computed 사용 시 원본 배열 변경하지 말 것.

  - computed에서 reverse() 및 sort() 사용시 원본 배열을 변경하기 때문에 복사본을 만들어서 진행 해야 함

    ```js
    // 이렇게 써야 함
    return [...numbers].reverse()
    
    //이렇게 쓰면 안됨
    return numbers.reverse() // 원본을 건드리면 안된다.
    ```



- 배열의 인덱스를 v-for의 key로 사용하지 말 것
  - 인덱스는 식별자가 아닌 배열의 항목 위치만 나타내기 때문에 Vue가 DOM을 변경할 때 (끝이 아닌 위치에 새 항목이 배열에 삽입되면) 여러 컴포넌트간 데이터 공유 시 문제가 발생
  - 직접 고유한 값을 만들어내는 메서드를 만들거나 외부 라이브러리 등을 활용하는 등 식별자 역할을 할 수 있는 값을 만들어 사용



---

#### 참고

- v-for와 배열 - "배열 변경 감지"

  - 수정 메서드 (원본 배열 수정)
    - Vue는 반응형 배열의 변경 메소드가 호출되는 것을 감지하여, 필요한 업데이트를 발생시킴
    - push, pop, shift, unshift, splice, sort, reverse
  - 배열 교체
    - 원본 배열을 수정하지 않고 항상 새 배열을 반환
    - filter, concat, slice

  

- v-for와 배열 -"필터링/정렬 결과 표시 "

  - 원본 데이터를 수정하거나 교체하지 않고 필터링 되거나 정렬된 결과를 표시

    1. computed 활용

    ```html
    <li v-for="number in evenNumbers">
      {{ number }}
    </li>
    
    const numbers = ref([1, 2, 3, 4, 5])
    const evenNumbers = computed(() => {
      return numbers.value.filter((number) => number % 2 === 0)
    })
    ```

    

    2. method 활용 (computed가 불가능한 중첩된 v-for에 경우)

    ```html
    <ul v-for="numbers in numberSets">
      <li v-for="num in evenNumberSets(numbers)">
        {{ num }}
      </li>
    </ul>
    
    const numberSets = ref([
      [1, 2, 3, 4, 5],
      [6, 7, 8, 9, 10],
    ])
    
    const evenNumberSets = function (numbers) {
      return numbers.filter((number) => number % 2 === 0)
    }
    ```

  

  

- TODOS

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  
  <body>
    <div id="app">
      <form @submit.prevent="addTodo">
        <input v-model="newTodo">
        <button>Add Todo</button>
      </form>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          {{ todo.text }}
          <button @click="removeTodo(todo)">X</button>
        </li>
      </ul>
    </div>
  
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      const { createApp, ref } = Vue
  
      const app = createApp({
        setup() {
          let id = 0
  
          const newTodo = ref(null)
          const todos = ref([
            { id: id++, text: 'Learn HTML' },
            { id: id++, text: 'Learn JS' },
            { id: id++, text: 'Learn Vue' }
          ])
  
          const addTodo = function () {
            todos.value.push({ id: id++, text: newTodo.value })
            newTodo.value = null
          }
  
          const removeTodo = function (todo) {
            todos.value = todos.value.filter((t) => t !== todo)
          }
  
          return {
            newTodo,
            todos,
            addTodo,
            removeTodo
          }
        }
      })
  
      app.mount('#app')
    </script>
  </body>
  
  </html>
  ```

  

- Cat Image

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  
  <body>
    <div id="app">
      <button @click="getCatImage">냥냥펀치</button>
    </div>
  
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      const { createApp, ref, onMounted } = Vue
      const URL = 'https://api.thecatapi.com/v1/images/search'
  
      const app = createApp({
        setup() {
          const getCatImage = function () {
            axios({
              method: 'get',
              url: URL,
            })
              .then((response) => {
                imgUrl = response.data[0].url
                return imgUrl
              })
              .then((imgData) => {
                imgElem = document.createElement('img')
                imgElem.setAttribute('src', imgData)
                document.body.appendChild(imgElem)
              })
              .catch((error) => {
                console.log('실패했다옹')
              })
          }
  
          onMounted(() => {
            getCatImage()
          })
  
          return {
            getCatImage
          }
        }
      })
  
      app.mount('#app')
    </script>
  </body>
  
  </html>
  
  ```
{% endraw %}
  