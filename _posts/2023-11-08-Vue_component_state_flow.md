---
title: Component State Flow
date: 2023-11-08 19:06:00 +09:00
categories: [Vue]
tags:
  [
    vue,
    Props,
    Emit,
    Static Props,
    Dynamic Props,
    Componnet Event,
  ]
---

# Component State Flow
{% raw %}
#### Passing Props

- 동일한 사진 데이터가 한 화면에 다양한 위치에서 여러 번 출력되고 있음

- 하지만 해당 페이지를 구성하는 컴포넌트가 여러 개라면 각 컴포넌트가 개별적으로 동일한 데이터를 관리해야 할까?

- 그렇다면 사진을 변경 해야 할 때 모든 컴포넌트에 대해 변경 요청을 해야 함

  > "공통된 부모 컴포넌트에서 관리하자"



- 부모는 자식에게 데이터를 전달(Pass Props)하며, 자식은 자신에게 일어난 일을 부모에게 알림(Emit event)



- Props

  - 정의 : 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달하는데 사용되는 속성

  - 특징

    - 부모 속성이 업데이트되면 자식으로 흐르지만 그 반대는 안됨
    - 즉, 자식 컴포넌트 내부에서 props를 변경하려고 시도해서는 안되며 불가능
    - 또한 부모 컴포넌트가 업데이트될 때마다 자식 컴포넌트의 모든 props가 최신 값으로 업데이트 됨

    > 부모 컴포넌트만 변경하고 이를 내려받는 자식 컴포넌트는 자연스럽게 갱신



- One-Way Data Flow
  - 모든 props는 자식 속성과 부모 속성 사이에 하향식 단방향 바인딩을 형성
  - one-way-down-binding



- 단방향인 이유

  하위 컴포넌트가 실수로 상위 컴포넌트의 상태를 변경하여 앱에서의 데이터 흐름을 이해하기 어렵게 만드는 것을 방지하기 위함





---

#### 실습

- 사전 준비
  - vue 프로젝트 생성(npm create vue@latest)
  - 초기 생성된 컴포넌트 모두 삭제(App.vue 제외)
  - src/assets 내부 파일 모두 삭제
  - main.js에 css관련 코드 삭제
  - 해당 문서에서 P(Parent), PC(ParentChild), PGC(ParentGrandChild)로 표시



- App > Parent > ParentChild 컴포넌트 관계 작성

  - App 컴포넌트 작성

  ```html
  <!-- APP.vue -->
  <template>
    <div>
      <Parent />
    </div>
  </template>
  
  <script setup>
  import Parent from '@/components/Parent.vue'
  </script>
  ```

  

  - Parent 컴포넌트 작성

  ```html
  <!-- Parent.vue -->
  <template>
      <div>
          <ParentChild />
      </div>
  </template>
  
  <script setup>
  import ParentChild from '@/components/ParentChild.vue';
  </script>
  ```

  

  - ParentChild 컴포넌트 작성

  ```html
  <!-- PrentChild.vue -->
  <template>
      <div>
      </div>
  </template>
  
  <script setup>
  </script>
  ```

  

- Props 선언

  -  부모 컴포넌트에서 보낸 props를 사용하기 위해서는 자식 컴포넌트에서 명시적인 props 선언이 필요

  

  - 부모 컴포넌트 Parent에서 자식 컴포넌트 ParentChild에 보낸 props 작성

  ```html
  <!-- Parent.vue -->
  <template>
      <div>
          <ParentChild my-msg="message" />
      </div>
  </template>
  ```

  my-msg : prop 이름 (케밥케이스, html의 attribute에서 대소문자 구분을 하지 않기 때문에, 가독성과 협업을 위해 소문자로 작성하기 때문)

  "message" : prop 값



- Props 선언 2가지 방식 

  1. 문자열 배열을 사용한 선언

     - defineProps()를 사용하여 props 선언

     ```html
     <!-- PrentChild.vue -->
     
     <script setup>
     defineProps(['myMsg'])
     </script>
     ```

     

  2. 객체를 사용한 선언(사용 권장)

     - 객체 선언 문법의 각 객체 속성의 키는 props의 이름이 되며, 객체 속성의 값은 값이 될 데이터의 타입에 해당하는 생성자 함수(Number, String..)여야 함

     ```html
     <!-- PrentChild.vue -->
     
     <script setup>
     defineProps({
         myMsg: String,
     })
     </script>
     ```

     

- prop 데이터 사용

  - 템플릿에서 반응형 변수와 같은 방식으로 활용

  ```html
  <!-- PrentChild.vue -->
  <template>
      <div>
          <p>{{ myMsg }}</p>
      </div>
  </template>
  
  <script setup>
  // props를 객체로 반환하므로 필요한 경우 JavaScript에서 접근 가능
  const props = defineProps({
                  myMsg: String,
                 })
  console.log(props.myMsg) // 'message'
  </script>
  ```

  

- 한 단계 더 prop 내려 보내기

  - ParentChild 컴포넌트를 부모로 갖는 ParentGrandChild 컴포넌트 생성 및 등록

  ```html
  <!-- ParentGrandChild.vue -->
  <template>
      <div>
      </div>
  </template>
  ```

  ```html
  <!-- PrentChild.vue -->
  <template>
      <div>
          <p>{{ myMsg }}</p>
          <ParentGrandChild />
      </div>
  </template>
  
  <script setup>
  import ParentGrandChild from '@/components/ParentGrandChild.vue'
  
  defindProps({
      myMsg: String,
  })
  </script>
  ```

  

  - ParentChild 컴포넌트에서 Parent로부터 받은 prop인 myMsg를 ParentGrandChild에게 전달

  ```html
  <!-- PrentChild.vue -->
  <template>
      <div>
          <p>{{ myMsg }}</p>
          <!-- v-bind를 사용한 동적 props -->
          <ParentGrandChild :my-msg="myMsg" />
      </div>
  </template>
  
  ```

  ```html
  <!-- ParentGrandChild.vue -->
  <template>
      <div>
          <p>{{ myMsg }}</p>
      </div>
  </template>
  
  <script setup>
  defineProps({
      myMsg: String,
  })
  </script>
  ```

  

  - PGC가 받아서 출력하는 prop은 P에 정의 되어 있는 prop이며 P가 prop을 변경할 경우 이를 전달받고 있는 PC, PGC에서도 모두 업데이트 됨



- Props 세부사항

  1. Props Name Cahing (Props 이름 컨벤션)

     - 선언 및 참조 시(카멜 케이스)

     ```html
     <p>{{ myMsg }}</p>
     ```

     ```js
     definProps({
         myMsg: String
     })
     ```

     

     - 자식 컴포넌트로 전달시(케밥 케이스)

     ```html
     <ParentChild my-msg="message"
     ```

     기술적으로 camelCase도 가능하나 HTML 속성 표기법과 동일하게 kebab-case로 표기할 것을 권장

     

  2. Static Props & Dynamic Props

     - 지금까지 작성한 것은 Static(정적) props
     - v-bind를 사용하여 동적으로 할당된 props를 사용할 수 있음

     

     - Dynamic props 정의

     ```html
     <!-- Parent.vue -->
     <ParentChild my-msg="message" :dynamic-props="name" />
     
     <script setup>
     import { ref } from 'vue'
     const name = ref('Alice')
     </script>
     ```

     

     - Dynamic props 선언 및 출력

     ```html
     <!-- PrentChild.vue -->
     
     <p>{{ dynamicProps }}</p>
     
     <script setup>
     defineProps({
         myMsg: String,
         dynamicProps: String,
     })
     </script>
     ```

     

---

#### Component Events



- 부모는 자식에게 데이터를 전달(Pass Props)하며, 자식은 자신에게 일어난 일을 부모에게 알림(Emit event)

  > 부모가 prop 데이터를 변경하도록 소리쳐야 한다.



- $emit()
  - 자식 컴포넌트가 이벤트를 발생시켜 부모 컴포넌트로 데이터를 전달하는 역할의 메서드
  - '$' 표기는 Vue 인스턴스나 컴포넌트 내에서 제공되는 전역 속성이나 메서드를 식별하기 위한 접두어



- emit 메서드 구조

  > $emit(event, ...args)

  - event : 커스텀 이벤트 이름
  - args : 추가 인자



- 이벤트 발신 및 수신(Emitting and Listening to Events)

  - $emit을 사용하여 템플릿 표현식에서 직접 사용자 정의 이벤트를 발식

  ```html
  <!-- PrentChild.vue -->
  <button @click="$emit('someEvent')">클릭</button>
  ```

  - 그러면 부모는 v-on을 사용하여 수신할 수 있음

  ```html
  <!-- Parent.vue -->
  <ParentChild @some-event="someCallback" />
  ```



- 이벤트 발신 및 수신

  - ParentChild에서 someEvent라는 이름의 사용자 정의 이벤트를 발신

  ```html
  <!-- PrentChild.vue -->
  
  <button @click="$emit('someEvent')">클릭</button>
  ```

  

  - ParentChild의 부모 Parent는 v-on을 사용하여 발신된 이벤트를 수신
  - 수신 후 처리할 로직 및 콜백 함수 호출

  ```html
  <!-- Parent.vue -->
  
  <ParentChild my-msg="message" :dynamic-props="name" 
          @some-event="someCallback"
          />
  
  <script>
  const someCallback = function(){
      console.log('ParentChild가 발생한 emit 이벤트를 수신했습니다.')
  }
  </script>
  ```



- 'emit'Event 선언

  - defineEmits()를 사용하여 명시적으로 발신할 이벤트를 선언할 수 있음
  - script에서 $emit 메서드를 접근할 수 없기 때문에 defineEmits()는 $emit 대신 사용할 수 있는 동등한 함수를 반환

  ```html
  <script setup>
  const emit = defineEmits(['someEvent'])
  const buttonClick = function(){
      emit('someEvent')
  }
  </script>
  ```



- 이벤트 선언하기

  - 이벤트 선언 방식으로 추가 버튼 작성 및 결과 확인

  ```html
  <!-- PrentChild.vue -->
  <button @click="buttonClick">클릭</button>
  
  <script setup>
  const emit = defineEmits(['someEvent'])
  const buttonClick = function(){
      emit('someEvent')
  }
  </script>
  ```

  

- 이벤트 인자(Event Arguments)

  - 이벤트 발신 시 추가 인자를 전달하여 값을 제공할 수 있음

  

  - PC에서 이벤트를 발신하여 P로 추가 인자 전달하기

  ```html
  <!-- PrentChild.vue -->
  <button @click="emitArgs">추가 인자 전달</button>
  
  <script setup>
  const emit = defineEmits(['someEvent', 'emitArgs'])
  const emitArgs = function(){
      emit('emitArgs', 1, 2, 3)
  }
  </script>
  ```

  

  - PC에서 발신한 이벤트를 P에서 수신

  ```html
  <!-- Parent.vue -->
  <template>
      <div>
          <ParentChild 
          my-msg="message" 
          :dynamic-props="name" 
          @some-event="someCallback"
          @emit-args="getNumbers"
          />
      </div>
  </template>
  
  <script setup>
  const getNumbers = function(...args){
      console.log(args)
      console.log(`ParentChild가 전달한 추가인자 ${args}를 수신했어요.`)
  }
  </script>
  ```



- Event Name Cashing

  - 선언 및 발신 시(camelCase)

  ```html
  <button @click="$emit('someEvent')">클릭</button>
  
  <script setup>
  const emit = defineEmits(['someEvent'])
  
  const buttonClick = function(){
      emit('someEvent')
  }
  </script>
  ```

  

  - 부모 컴포넌트에서 수신시(kebab-case)

  ```html
  <ParentChild @some-event="..." />
  ```

  

- emit 이벤트 실습

  - 최하단 컴포넌트 PGC에서 P컴포넌트의 name 변수 변경 요청하기

  ```
  App - Parent - ParentChild - ParentGrandChild
  와 같은 구조일 때
  한번에 2단계 emit은 불가능.
  PGC에서 PC로 emit하고 PC에서 P로 다시 한 번 emit 해야 한다.
  ```

  

  - PGC에서 이름 변경을 요청하는 이벤트 발신

  ```html
  <!-- ParentGrandChild.vue -->
  
  <button @click="updateName">이름 변경!</button>
  
  <script setup>
  const emit = defineEmits(['updateName'])
  
  const updateName = function() {
      emit('updateName')
  }
  </script>
  ```

  

  - 이벤트 수신 후 이름 변경을 요청하는 이벤트 발신

  ```html
  <!-- PrentChild.vue -->
  
  <template>
      <div>
          <p>{{  myMsg }}</p>
          <p>{{ dynamicProps }}</p>
          <ParentGrandChild :my-msg="myMsg" 
          @update-name="updateName"
          />
      </div>
  </template>
  
  <script setup>
  const emit = defineEmits(['someEvent', 'emitArgs', 'updateName'])
  
  const updateName = function (){
      emit('updateName')
  }
  </script>
  ```

  

  - 이벤트 수신 후 이름 변수 변경 메서드 호출
  - 해당 변수를 prop으로 받는 모든 곳에서 자동 업데이트

  ```html
  <!-- Parent.vue -->
          <ParentChild @update-name="updateName" />
  
  <script setup>
  const updateName = function() {
      name.value='Bella'
  }
  </script>
  ```

  

---

#### 참고

- 첫 번째는 정적 props로 문자열로써의 "1"을 전달
- 두 번째는 동적 props로 숫자로써의 1을 전달

```html
<!-- 1 -->
<SomeComponent num-props="1" />
<!-- 2 -->
<SomeComponent :num-props="1" />
```



- Prop 선언을 객체 선언 문법으로 권장하는 이유

  - prop에 타입을 지정하는 것은 컴포넌트를 가독성이 좋게 문서화하는데 도움이 된다.
  - 다른 개발자가 잘못된 유형을 전달할 때에 브라우저 콘솔에 경고를 출력하도록 함
  - prop에 대한 유효성 검사로써 활용 가능
  - https://vuejs.org/guide/components/props.html#prop-validation 참고

  ```js
  defineProps({
      // 여러 타입 허용
      propB: [String, Number],
      
      // 문자열 필수
      propC: {
          type: String,
          required: true
      },
      
      // 기본 값을 가지는 숫자형
      propD: {
          type: Number,
          default: 10
      },
  })
  ```

  

- emit 이벤트도 객체 선언 문법으로 작성 가능

  - props 타입 유효성 검사와 유사하게 emit 이벤트 또한 객체 구문으로 선언 된 경우 유효성을 검사할 수 있음

  ```js
  const emit = defineEmits({
      // 유효성 검사 없음
      click: null,
      
      // submit 이벤트 유효성 검사
      submit: ({ email, password }) => {
          if (email && password) {
              return true
          } else {
              console.warn('submit 이벤트가 옳지 않음')
              return false
          }
      }
  })
  const submitForm = function (email, password) {
      emit('submit', { email, password })
  }
  ```
  {% endraw %}