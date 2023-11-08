---
title: JavaScript Reference Data Types
date: 2023-10-25 19:06:00 +09:00
categories: [JavaScript]
tags:
  [
    javascript,
    object,
    reduce,

  ]
---

# JavaScript Reference Data Types

#### 함수

- Function

  참조 자료형에 속하며 모든 함수는 Function object이다.

  참조 자료형 : 객체의 주소가 저장되는 자료형(가변, 주소가 복사)



- 함수 정의

  - 함수 구조 

    함수의 이름, 매개변수, body를 구성하는 statement

    return 값이 없다면 undefined를 반환

    ```js
    function name ([param[,param,[..., param]]]) {
        statements
        return value
    }
    ```

  

  - 함수 정의 2가지 방법

    - 선언식(function declaration)
      ```js
      function add(num1, num2) {
          return num1 + num2
      }
      add(1, 2) // 3
      ```

      

    - 표현식(function expression)
      ```js
      const sub = function(num1, num2) {
          return num1 - num2
      }
      sub(2, 1) // 1
      ```

      

  - 함수 표현식 특징

    함수 이름이 없는 '익명 함수'를 사용할 수 있음

    선언식과 달리 표현식으로 정의한 함수는 호이스팅 되지 않음으로 함수를 정의하기 전에 먼저 사용할 수 없다.

    ```js
    console.log(add(1, 2)) //3
    
    function add(num1, num2){
      return num1 + num2
    }
    ```

    ```js
    sub(2, 1)
    // "ReferenceError: Cannot access 'sub' before initialization"
    
    const sub = function (num1, num2) {
        return num1 - num2
    }
    ```

    

  - 함수 선언식과 표현식 종합

    |      |                    선언식                     |                            표현식                            |
    | :--: | :-------------------------------------------: | :----------------------------------------------------------: |
    | 특징 | 익명 함수 사용 불가능<br />함수 호이스팅 발생 | 익명 함수 사용 가능<br />변수 호이스팅 발생했으나 const 때문에 에러 발생 |
    | 기타 |                                               |                          사용 권장                           |



- 매개변수

  - 매개변수 정의 방법

    1. 기본 함수 매개변수(Default function parameter)

       값이 없거나 undefined가 전달될 경우 이름 붙은 매개변수를 기본값으로 초기화

       ```js
       const greeting = function (name = 'Anonymous') {
           return `Hi ${name}`
       }
       greeting() // Hi Anonymous
       ```

       

    2. 나머지 매개 변수

       임의의 수의 인자를 배열로 허용하여 가변 인자를 나타내는 방법

       ```js
       /*
       작성규칙
       1. 함수 정의 시 나머지 매개변수 하나만 작성할 수 있음
       2. 나머지 매개변수는 함수 정의에서 매개변수 마지막에 위치해야 함
       */
       const myFunc = function (param1, param2, ...restPrams) {
           return [param1, param2, restParams]
       }
       myFunc(1, 2, 3, 4, 5) // [1, 2, [3, 4, 5]]
       myFunc(1, 2) // [1, 2, []]
       ```

       

- 매개변수와 인자의 개수 불일치

  매개변수 개수가 인자 개수보다 많을 경우 누락된 인자는 undefined로 할당

  ```js
  const threeArgs = function (param1, param2, param3) {
      return [param1, param2, param3]
  }
  threeArgs(1) // [1, undefiend, undefind]
  threeArgs(2, 3) // [2, 3, undefind]
  ```


  초과 입력한 인자는 사용하지 않음

  ```js
  const twoArgs = functions(param1, param2) {
      return [param1, param2]
  }
  twoArgs(1, 2, 3) // [1, 2]
  ```

  

- Spread syntax

  '...' : 전개구문

  - 배열이나 문자열 같이 반복 가능한 항목을 펼치는 것 (확장, 전개)

  - 전개 대상에 따라 역할이 다름

    배열이나 객체의 요소를 개별적인 값으로 분리하거나 다른 배열이나 객체의 요소를 현재 배열이나 객체에 추가하는 등

  - 함수와의 사용

    함수 호출 시 인자 확장, 나머지 매개변수(압축)

  - 객체와의 사용

  - 배열과의 활용



- 전개구문 활용

  ```js
  // 함수 호출 시 인자 확장
  function myFunc(x, y, z) {
      return x + y + z
  }
  let numbers = [1, 2, 3]
  console.log(myFunc(...numbers)) // 6
  ```

  ```js
  // 나머지 매개변수 (압축)
  function myFunc2(x, y, ...restArgs){
      return [x, y, restArgs]
  }
  console.log(myFunc2(1, 2, 3, 4, 5)) // [1, 2, [3, 4, 5]]
  console.log(myFunc2(1, 2))  [1, 2, []]
  ```



- 화살표 함수(중요, 권장)

  함수 표현식의 간결한 표현법

  ```js
  const arrow = function(name){
      return `hello, ${name}`
  }
  // 아래와 같이 바꿀 수 있음
  const arrow = name => `hello, ${name}`
  ```

  

  - 작성과정
    1. function 키워드 제거 후 매개변수와 중괄호 사이에 화살표 작성
    2. 함수의 매개변수가 하나 뿐이라면 매개 변수의 '()' 제거 가능(단, 생략하지 않는 것을 권장)
    3. 함수 본문의 표현식이 한 줄이라면 '{}' 와 'return' 제거 가능

---

####  참고 : 화살표 함수 심화

```js
// 1. 인자가 없다면 () or _ 로 표시 가능
const noArgs1 = () => 'No args'
const noArgs2 = _ => 'No args'

// 2-1. object를 return 한다면 return 을 명시적으로 작성해야 함
const returnObject = () => { return { ket: 'value' } }

// 2-2. return을 작성하지 않으려면 객체를 소괄호로 감싸야 함
const returnObject2 = () => ({ key: 'value' })
```

---

#### 객체

- Object

  키로 구분된 데이터 집합을 저장하는 자료형



- 객체 구조

  - 중괄호를 이용해 작성

  - 중괄호 안에는 'key:value' 쌍으로 구성된 속성을 여러 개 작성 가능

  - key는 문자형만 허용, value는 모든 자료형 허용

  ```js
  const user = {
      name: 'Alice',
      'key with space' : true,
      greeting: function() {
          return 'hello'
      }
  }
  ```



- 속성 참조

  - 점 또는 대괄호로 객체 요소 접근
  - key이름에 띄어쓰기 같은 구분자가 있으면 대괄호 접근만 가능

  ```js
  // 조회
  console.log(user.name) // Alice
  console.log(user['key with space']) // true
  
  // 추가
  uesr.address = 'korea'
  
  // 수정
  user.name = 'Bella'
  console.log(user.name) // Bella
  
  // 삭제
  delete user.name
  ```

  

- in 연산자

  속성이 객체에 존재하는지 여부를 확인

  ```js
  console.log('greeting' in user) // true
  console.log('contry' in user) // false
  ```



- Method

  객체 속성에 정의된 함수

  

  - Method 사용 예시

    object.method() 방식으로 호출

    메서드는 객체를 '행동'할 수 있게 함

    ```js
    console.log(user.greeting()) // hello
    ```

  

- 'this keyword

  - 자기 참조 변수

    > 자기 참조 변수는 자신이 어떻게 "호출"되는 가에 따라서 다르다.
    >
    > a() / ~a.() / new a() / ~~~.call(a)  / ~.apply(a) / ~.bind(a)
    >
    > 호출되는가? or 전달되는가? 에 따라서 달라지는 것을 확인
  
    
  
  - "호출"되는 방식에 따라 다르다.
  
  함수나 메서드를 호출한 객체를 가리키는 키워드
  
  'this'키워드를 사용해 객체에 대한 특정한 작업을 수행 할 수 있음
  
  : 함수 내에서 객체의 속성 및 메서드에 접근하기 위해 사용



- Method & this 사용 예시

  ```js
  const person = {
      name : 'Alice',
      greeting : function () {
          return `Hello my name is ${this.name}`
      },
  }
  
  console.log(person.greeting()) // Hello my name is Alice
  ```

  ```
  JavaScript에서 this는 함수를 호출하는 방법에 따라 가리키는 대상이 다르다.
  
  단순 호출 : 전역 개체
  메서드 호출 : 메서드를 호출한 객체
  ```

  ```js
  // 1. 단순 호출 시 this (일반 함수로 호출 되었을 때 => this는 전역 객체)
  // 가리키는 대상 => 전역 객체
  const myFunc = function() {
      return this
  }
  console.log(myFunc()) // window
  
  // 2. 메서드 호출 시 this
  // 가리키는 대상 => 메서드를 호출한 객체
  const myObj = {
      data: 1,
      myFunc: function(){
          return this
      }
  }
  console.log(myObj.myFunc()) // myObj
  ```

  ```js
  // 3. 생성자 함수(클래스)
  : new 호출되었을 때
  : this => 미래에 생성될 인스턴스
  ```

  ```js
  // 4. 중첩된 함수에서의 this 문제점과 해결책
  const myObj2 = {
      numbers: [1, 2, 3],
      myFunc: function(){
          this.numbers.forEach(function(number){
              console.log(this) // window
          })
      }
  }
  console.log(myObj2.myFunc())
  // forEach의 인자로 작성된 콜백 함수는 일반적인 함수 호출이기 때문에 this가 전역 객체를 가리킴
  ```

  ```js
  const myObj3 = {
      numbers : [1, 2, 3],
      myFunc: function() {
          this.numbers.forEach((number) => {
              console.log(this) //myObj3
          })
      }
  }
  console.log(myObj3.myFunc())
  // 화살표 함수는 자신만의 this를 가지지 않기 때문에 외부 함수에서의 this 값을 가져옴.
  
  //화살표 함수의 this는 '렉시컬 this'라고 하며, "바로 위의" this를 따라간다.
  ```

  ```js
  // 5. 간접 호출 되었을 때
  // function.prototype.apply/call/bind 메서드에 의한 간접 호출 -> 메서드의 첫번째 인자
  ```

  

- JavaScript 'this' 정리
  - JS에서 this는 함수가 '호출되는 방식'에 따라 결정되는 현재 객체를 나타냄
  - JS의 함수는 호출될 때 this를 암묵적으로 전달 받음
  - python의 self와 Java의 this가 선언 시 값이 이미 정해지는 것에 비해 JS의 this는 함수가 호출되기 전까지 값이 할당되지 않고, 호출 시에 결정됨(동적 할당)



- 추가 객체 문법

  - 단축 속성

  ```js
  // 키 이름과 값으로 쓰이는 변수의 이름이 같은 경우 단축 구문을 사용할 수 있음
  
  const name = 'Alice'
  const age = 30
  
  const user = {
      name : name,
      age : age,
  }
  // 아래와 같이 변할 수 있음
  const user = {
      name, 
      age,
  }
  ```

  

  - 단축 메서드

  ```js
  // 메서드 선언 시 function 키워드 생략 가능
  const myObj1 = {
      myFunc: function() {
          return 'Hello'
      }
  }
  //아래와 같이 변할 수 있음
  const myObj2 = {
      myFunc() {
          return 'Hello'
      }
  }
  ```

  

  - 계산된 속성

  ```js
  // 키가 대괄호로 둘러쌓여 있는 속성
  // 고정된 값이 아닌 변수 값을 사용할 수 있음
  
  const product = prompt('물건 이름을 입력해주세요')
  const prefix = 'my'
  const suffix = 'property'
  
  const bag = {
      [product] : 5,
      [prefix + suffix]: 'value',
  }
  console.log(bag) // {연필: 5, myproperty: 'value'}
  ```

  

  - 구조 분해 할당(중요)

  ```js
  // 배열 또는 객체를 분해하여 속성을 변수에 쉽게 할당할 수 있는 문법
  const userInfo = {
      firstName : 'Alice',
      userId : 'alice123',
      email : 'alice123@gmail.com',
  }
  const firstName = userInfo.firstName
  const userId = userInfo.userId
  const email = userInfo.email
  
  // =>
  const userInfo = {
      firstName: 'Alice',
      userId: 'alice123',
      email: 'alice123@gmail.com'
  }
  
  const { firstName } = userInfo
  const { firstName, userId } = userInfo
  const { firstName, userId, email } = userInfo
  
  // Alice alice123 alice123@gmail.com
  console.log(firstName, userId, email)
  ```

  ```js
  function printInfo({name, age, city}) {
      console.log(`이름: ${name}, 나이: ${age}, 도시: ${city}`)
  }
  
  const person = {
      name: 'Bob',
      age: 35,
      city: 'London',
  }
  //함수 호출 시 객체를 구조 분해하여 함수의 매개변수로 전달
  printInfo(person) // 이름: Bob, 나이:35, 도시: London
  ```
  
  
  
  - Object with '전개 구문'
  
    객체 복사 : 객체 내부에서 객체 전개
  
    얕은 복사에 활용 가능
  
  ```js
  const obj = {b: 2, c: 3, d: 4}
  const newObj = {a: 1, ...obj, e:5}
  console.log(newObj) // {a: 1, b: 2, c: 3, d: 4, e: 5}
  ```
  
  
  
  - 유용한 객체 매서드
  
    Object.keys()
  
    Object.vlaues()
  
  ```js
  const profile = {
      name: 'Alice',
      age: 30,
  }
  console.log(Object.keys(profile)) // ['name', 'age']
  console.log(Object.values(profile)) // ['Alice', 30]
  ```
  
  
  
  - Optional chaining('?.')
  
    속성이 없는 중첩 객체를 에러 없이 접근할 수 있음
  
    만약 참조 대상이 null 또는 undefined라면 에러가 발생하는 것 대신 평가를 멈추고 undefined를 반환
  
  
    ```js
    const user = {
        name: 'Alice',
        greeting: function (){
            return 'hello'
        }
    }
    
    console.log(user.address.street) // Uncaught TypeError
    console.log(user.address?.street) // undefined
    
    console.log(user.nonMethod()) // Uncaught TypeError
    conosle.log(user.nonMethod?.()) //undefined
    ```
  
    ```js
    // Optional chaining이 없다면 다음과 같이 '&&'연산자를 사용해야 함
    console.log(user.address && user.address.street) // undefined
    ```
  
    - 장점
  
    참조가 누락될 가능성이 있는 경우 연결된 속성으로 접근할 때 더 짧고 간단한 표현식을 작성 가능
  
    어떤 속성이 필요한지에 대한 보증이 확실하지 않는 경우에 객체의 내용을 보다 편리하게 탐색할 수 있음
  
    
  
    - 주의사항
  
    Optional chaining은 존재하지 않아도 괜찮은 대상에만 사용(남용하지 말 것)
  
    ```js
    // 왼쪽 평가대상이 없어도 괜찮은 경우에만 선택적으로 사용
    // 이전 예시 코드에서 user 객체는 논리상 반드시 있어야 하지만 address는 필수 값이 아님
    // user에 값을 할당하지 않은 문제가 있을 때 바로 알아낼 수 있어야 하기 때문
    
    // bad
    user?.address?.street
    
    // good
    user.address?.street
    ```
  
    Optional chaining 앞의 변수는 반드시 선언되어 있어야 함
  
    ```js
    console.log(myObj?.address)
    // Unchangt ReferenceError : myObj is not defined
    ```
  
    
  
  - Optional chaining 요약
  
    - obj?.prop
  
      obj가 존재하면 obj.prop을 반환하고, 그렇지 않으면 undefined를 반환
  
    
  
    - obj?.[prop]
  
      obj가 존재하면 obj[prop]를 반환하고, 그렇지 않으면 undefined를 반환
  
    
  
    - obj?.method()
  
      obj가 존재하면 obj.method()를 호출하고, 그렇지 않으면 undefined를 반환
  
    



- JSON
  - JavaScript Object Notation
  - Key - Value 형태로 이루어진 자료 표기법
  - JS의 Object와 유사한 구조를 가지고 있지만 JSON 형식은 "문자열"
  - JS에서 JSON을 사용하기 위해서는 Object 자료형으로 변경해야 함



- Object < > JSON 변환하기

  ```js
  const jsObject = {
      coffee: 'Americano',
      iceCream: 'Cookie and Cream',
  }
  ```

  ```js
  // Object -> Json
  const objToJson = JSON.stringify(jsObject)
  console.log(objToJson) // {"coffee":"Americano", "iceCream":"Cookie and Cream"}
  console.log(typeof objToJson) // string
  ```

  ```js
  // JSON -> Object
  const jsonToObj = JSON.parse(objToJson)
  console.log(jsonToObj) // {coffee: 'Americano', iceCream: 'Cooke and Cream'}
  console.log(typeof jsonToObj) // object
  ```



---

#### 참고

- new 연산자

  - JS에서 객체를 하나 생성한다고 한다면?

    하나의 객체를 선언하여 생성

  - 동일한 형태의 객체를 또 만든다면?

    또 다른 객체를 선언하여 생성해야 함

  - 이런 불편함을 해결하기 위한 new 연산자

  - 사용자 정의 객체 타입을 생성

  - 매개 변수

    1. constructor : 객체 인스턴스의 타입을 기술(명세)하는 함수
    2. arguments : constructor와 함께 호출될 값 목록

    ```js
    new constructor[([arguments])]
    ```

  - 활용

  ```js
  // 생성자 함수 첫 글자는 대문자로(약속)
  function Member(name, age, sId) {
      this.name = name
      this.age = age
      this.sId = sId
  }
  
  const member3 = new Member('Bella', 21, 20226543)
  ```



- JS 'this'의 장단점
  - this가 미리 정해지지 않고 호출 방식에 의해 결정되는 것
    - 장점 : 함수(메서드)를 하나만 만들어 여러 객체에서 재사용할 수 있다는 것
    - 단점 : 이런 유연함이 실수로 이어질 수 있다는 것
  - 개발자는 this의 동작 방식을 충분히 이해하고 장점을 취하면서 실수를 피하는 데에 집중



---

#### 배열

- Object

  키로 구분된 데이터 집합(data collection)을 저장하는 자료현



- Array

  순서가 있는 데이터 집합을 저장하는 자료 구조



- 배열 구조

  - 대괄호([ ])를 이용해 작성
  - 배열 요소 자료형 : 제약 없음
  - length 속성을 사용해 배열에 담긴 요소가 몇 개인지 알 수 있음

  ```js
  const names = ['Alice', 'Bella', 'Cathy']
  
  console.log(name[0]) // Alice
  console.log(names.length) // 3
  ```

  

- 배열의 주요 메서드

  - push / pop : 배열 끝 요소를 추가 / 제거
  - unshift / shift : 배열 앞 요소를 추가 / 제거

  

  - pop()

  ```js
  // 배열 끝 요소를 제거하고,  제거한 요소를 반환
  
  console.log(names.pop()) // Cathy
  console.log(names) // ['Alice', 'Bella']
  ```

  

  - push()

  ```js
  // 배열 끝에 요소 추가
  names.push('Dan')
  console.log(names) // ['Alice', 'Bella', 'Dan']
  ```

  

  - shift()

  ```js
  // 배열 앞 요소를 제거하고, 제거한 요소를 반환
  console.log(names.shift()) // Alice
  console.log(names) // ['Bella', 'Dan']
  ```

  

  - unshift()

  ```js
  // 배열 앞에 요소를 추가
  name.unshift('Eric')
  console.log(names) // ['Eric', 'Bella', 'Dan']
  ```

  

- Array Helper Methods

  배열을 순회하며 특정 로직을 수행하는 메서드

  : 메서드 호출 시 인자를 함수(콜백 함수)로 받는 것이 특징



- 주요 Array Helper Methods

  - forEach : 인자로 주어진 함수(콜백 함수)를 배열 요소 각각에 대해 실행
  - map : 배열 내의 모든 요소 각각에 대해 함수(콜백 함수)를 호출하고, 함수 호출 결과를 모아 새로운 배열을 반환

  ---

  - forEach

  ```js
  arr.forEach(callback(item[, index[, array]]))
  ```

  콜백 함수는 3가지 매개변수로 구성

  1. item : 처리할 배열의 요소
  2. index : 처리할 배열 요소의 인덱스(선택 인자)
  3. array : forEach를 호출한 배열 (선택 인자)

  반환 값 : undefined

  ```js
  array.forEach(function (item, index, array) {
      // do something
  })
  ```

  

  - 활용

  ```js
  const names = ['Alice', 'Bella', 'Cathy',]
  
  // 일반 함수 표기
  names.forEach(function (item, index, array) {
      console.log(`${item} / ${index} / ${array}`)
  })
  
  // 화살표 함수 표기
  names.forEach((item, index, array) => {
      console.log(`${item} / ${index} / ${array}`)
  })
  ```

  ```js
  // 출력 결과
  Alice / 0 / Alice, Bella, Cathy
  Alice / 1 / Alice, Bella, Cathy
  Alice / 2 / Alice, Bella, Cathy
  ```



- 콜백 함수

  다른 함수에 인자로 전달되는 함수

  : 외부 함수내에서 호출되어 일종의 루틴이나 특정 작업을 진행

  

  - 예시

  ```js
  const numbers1 = [1, 2, 3]
  
  numbers1.forEach(function (num) {
      console.log(num ** 2)
  })
  // 1
  // 4
  // 9
  ```

  ```js
  const numbers2 = [1, 2, 3]
  const callBackFunction = function (num) {
      console.log(num ** 2)
  }
  numvers2.forEach(callBackFunction)
  // 출력 결과 위와 같음
  ```

---

- map()

  배열 내의 모든 요소 각각에 대해 함수(콜백 함수)를 호출하고, 함수 호출 결과를 모아 새로운 배열을 반환



- map 구조

  ```js
  arr.map(callback(item[, index[, array]]))
  ```

  1. itme : 처리할 배열의 요소

  2. index : 처리할 배열 요소의 인덱스 (선택 인자)

  3. array : map을 호출한 배열 (선택 인자)

     - 반환 값 : 배열의 각 요소에 대해 실행한 'callback의 결과를 모은 새로운 배열'

       : 기본적으로 forEach 동작 원리와 같지만 forEach와 달리 새로운 배열을 반환함


  ```js
  const newArr = array.map(function (item, index, array){
      // do something
  })
  ```

  

- map 활용

  ```js
  const names = ['Alice', 'Bella', 'Cathy']
  
  const result1 = names.map(function (name) {
      return name.length
  })
  
  const result2 = names.map((name) => {
      return name.length
  })
  
  console.log(result1) // [5, 5, 5]
  cnosole.log(result2) // [5, 5, 5]
  ```

  ```js
  const numbers = [1, 2, 3]
  
  const doubleNumber = numbers.map((number) => {
      return number * 2
  })
  console.log(doubleNumber) // [2, 4, 6]
  ```



- python에서의 map 함수와 비교

  - python의 map에 squrare 함수를 인자로 넘겨 numbers 배열의 각 요소를 square 함수의 인자로 ㅏㅅ용하였음

    ```python
    numbers = [1, 2, 3]
    def square(num):
        return num ** 2
    new_numbers = list(map(square, numbers))
    ```

  

  - map 메서드에 callBackFunc 함수를 인자로 넘겨 numbers 배열의 각 요소를 callBackFunc 함수의 인자로 사용하였음

    ```js
    const numbers = [1, 2, 3]
    
    const callBackFunction = function (number){
        return number ** 2
    }
    const newNumbers = numbers.map(callBackFunction)
    ```



- 배열 순회 종합

  ```js
  const name = ['Alice', 'Bella', 'Cathy']
  
  // for loop
  for (let idx = ; idx < names.length; idx++) {
      console.log(idx, names[idx])
  }
  
  // for ...of
  for (const name of names){
      console.log(name)
  }
  
  // forEach
  names.forEach((name, idx) => {
      conosle.log(idx, name)
  })
  ```

  | 방식          | 특징                                                         |
  | ------------- | ------------------------------------------------------------ |
  | for loop      | 배열의 인덱스를 이용하여 각 요소에 접근<br />break, continue 사용 가능 |
  | for ...of     | 배열 요소에 바로 접근 가능<br />break, continue 사용 가능    |
  | forEach<br /> | 간결하고 가독성이 높음<br />callback 함수를 이용하여 각 요소를 조작하기 용이<br />break, continue 사용 불가 |



- map 과 forEach의 차이.

  작동 자체는 큰 차이가 없지만 map은 반환값이 있다.

  잘 모르겠으면 메모리를 조금 포기하더라도 map을 쓰자

  ```js
  const a = [4, 5, 6]
  
  const b = a.map(item =>{
    return (item + 1)
  })
  console.log(b) // [5, 6, 7]
  
  const c = a.forEach(item =>{
    return item + 1
  })
  
  console.log(c) //undefined
  ```

  



---

#### 추가 배열 문법

- Array with '전개 구문'

  ```js
  // 배열 복사
  let parts = ['어깨', '무릎']
  let lyrics = ['머리', ...parts, '발']
  
  console.log(lyrics) // ['머리', '어깨', '무릎', '발']
  ```



- 기타 Array Helper Methods

  MDN 문서를 참고해 사용해보기

  - reduce : **`reduce()`** 메서드는 배열의 각 요소에 대해 주어진 리듀서 (reducer) 함수를 실행하고, '하나의 결과값'을 반환합니다. (누적값 출력할 때 용이)

  ```js
  const array1 = [1, 2, 3, 4];
  
  // 0 + 1 + 2 + 3 + 4
  //초기값
  const initialValue = 0;
  const sumWithInitial = array1.reduce((accumulator, currentValue, index, array) => {accumulator + currentValue}, initialValue);
  
  // 초기값에서 시작해서, 전값(acc)에 현재값(cur)를 더한다.
  
  console.log(sumWithInitial);
  // Expected output: 10
  ```

  - reduce 표 설명

  | acc    | 0    | 1    | 3    | 6    | 10   |
  | ------ | ---- | ---- | ---- | ---- | ---- |
  | cur    | 1    | 2    | 3    | 4    | 5    |
  | return | 1    | 3    | 6    | 10   | 15   |

  

  

  - filter : 콜백 함수의 반환 값이 참인 요소들만 모아서 새로운 배열을 반환

  ```js
  // 주어진 배열의 요소 중 특정 문자(query)가 포함되는 요소만 모아서 새로운 배열을 반환하시오.
  const languages = ['python', 'javascript', 'html', 'java']
  const query = 'java'
  const result = languages.filter((language) => language.includes(query));
  console.log(result);
  ```

  

  - find : 콜백 함수의 반환 값이 참이면 해당 요소를 반환

  ```js
  // 주어진 accounts 배열에서 balance가 24,000인 사람을 찾으시오.
  const accounts = [
    { name: 'sophia', balance: 1200 },
    { name: 'john', balance: 50000 },
    { name: 'tailer', balance: 24000 }
  ]
  
  const found = accounts.find((account) => account.balance == 24000);
  console.log(found)
  ```

  

  - some : 배열의 요소 중 하나라도 판별 함수를 통과하면 참을 반환

  ```js
  const array = [1, 2, 3, 4, 5];
  
  // Checks whether an element is even
  const even = (element) => element % 2 === 0;
  
  console.log(array.some(even));
  // Expected output: true
  
  ```

  

  - every : 배열의 모든 요소가 판별 함수를 통과하면 참을 반환

  ```js
  const isBelowThreshold = (currentValue) => currentValue < 40;
  
  const array1 = [1, 30, 39, 29, 10, 13];
  
  console.log(array1.every(isBelowThreshold));
  // Expected output: true
  ```

  

  - join

  ```js
  const elements = ['Fire', 'Air', 'Water'];
  
  console.log(elements.join());
  // Expected output: "Fire,Air,Water"
  
  console.log(elements.join(''));
  // Expected output: "FireAirWater"
  
  console.log(elements.join('-'));
  // Expected output: "Fire-Air-Water"
  ```

  



---

#### 참고

- 콜백 함수 구조를 사용하는 이유

  1. 함수의 "재사용성" 측면

     함수를 호출하는 코드에서 콜백 함수의 동작을 자유롭게 변경할 수 있음

     예를 들어, map 함수는 콜백 함수를 인자로 받아 배열의 각 요소를 순회하며 콜백 함수를 실행

     이때, 콜백 함수는 각 요소를 변환하는 로직을 담당하므로, map 함수를 호출하는 코드는 간결하고 가독성이 높아짐

  

  2. '비동기적 처리 측면'

     setTimeout 함수는 콜백 함수를 인자로 받아 일정 시간이 지난 후에 실행됨

     이때, setTimeout함수는 비동기적으로 콜백 함수를 실행하므로, 다른 코드의 실행을 방해하지 않음

     ```js
     console.log('a')
     setTimeout(()=>{
         console.log('b')
     }, 3000)
     console.log('c')
     // a
     // c
     // b (3초 후 실행)
     ```

     

- "배열은 객체다"

  - 배열은 키와 속성들을 담고 있는 참조 타입의 객체
  - 인덱스를 키로 가지며 length 프로퍼티를 갖는 특수한 객체
  - 배열의 요소를 대괄호 접근법을 사용해 접근하는 건 객체 문법과 같음
  - 다만 배열의 키는 숫자라는 점
  - 숫자형 키를 사용함으로써 배열은 객체 기본 기능 이외에도 순서가 있는 컬렉션을 제어하게 해주는 특별한 메서드를 제공

  ```js
  const names = ['Alice', 'Bella', 'Cathy']
  console.log(Object.getOwnPropertyDescriptors(names))
  /*
  
  [object Object] {
    0: [object Object] {configurable: true, enumerable: true, value: "Alice", writable: true},
    1: [object Object] {configurable: true, enumerable: true, value: "Bella", writable: true},
    2: [object Object] {configurable: true, enumerable: true, value: "Cathy", writable: true},
    length: [object Object] {configurable: false, enumerable: false, value: 3, writable: true}
  }
  */
  ```



- 메서드 : 객체 안에 있는 함수를 메서드라고 한다.



- input의 개수와 output의 수가 같다 => map
- input과 output의 조합을 보았을 때 개수가 1개 초과 => filter
- output이 필요 없다. => forEach(반환값 없음)
- output이 1개다. => reduce



---

#### 호이스팅

변수 호이스팅과 함수 호이스팅은 JavaScript에서 다르게 작동합니다. 변수 호이스팅은 변수 선언문만을 호이스팅하고 초기화(값 할당)는 호이스팅되지 않습니다. 따라서 `let`으로 선언한 변수는 호이스팅되어 스코프의 최상단으로 이동하지만 초기화되지 않기 때문에 호출 시 `undefined`가 됩니다.

반면 함수 호이스팅은 함수 선언문 전체가 호이스팅됩니다. 이것은 함수의 선언과 내용이 스코프의 최상단으로 끌어올려진다는 것을 의미합니다. 따라서 함수 선언 이전에 호출할 수 있습니다. 함수 선언문의 내용은 함께 호이스팅되므로 선언과 내용 모두 스코프 상단으로 올라갑니다.

```js
// 변수 호이스팅
console.log(a); // undefined
var a = 5;

// 함수 호이스팅
foo(); // 'Hello, world!'
function foo() {
  console.log('Hello, world!');
}
```





- import/require 호이스팅

  `import`문 및 `require`문은 해당 모듈 스코프의 최상단으로 호이스팅됩니다. 이것은 모듈을 가져오고 사용하기 전에 해당 모듈을 가져올 수 있음을 의미합니다.

  ```js
  import myModule from 'my-module';
  // 모듈 가져오기 및 사용
  ```

  



---

#### Reduce

```js
arr.reduce(calback[, initialValue])
```



- reduce 함수로 짝수만 선택

  ```js
  const a = [1, 2, 3, 4, 5];
  
  const b = a.reduce((acc, cur) => {
    if (cur % 2 === 0) {
      acc.push(cur);
    }
    return acc;
  }, []);
  
  console.log(b);
  ```

  

reduce() 메서드는 배열의 각 요소에 리듀서 함수를 실행, 하나의 결과값을 반환한다.

배열의 하나의 값으로 줄이기 때문에 reduce

- 누산기(accumulator) : 콜백의 반환값을 누적한다. 콜백 이전 반환 값 또는 콜백의 첫 번째 호출이면서 initialValue를 제공한 경우에는 initialValue의 값이다.
- 현재값(currentValue) : 처리할 현재 요소
- 현재 인덱스(currentIndex) : 처리할 현재 요소의 인덱스, initialValue를 제공한 경우 0, 아니면 1부터 시작한다.
- 원본 배열 (array) : reduce를 호출한 배열
- initialValue(optional) : callback 최초 호출에서 첫 번재 인수에 제공하는 값. 초기값을 제공하지 않으면 배열의 첫 번째 요소를 사용한다. 빈 배열에서 초기값 없이 reduce를 호출하면 오류가 발생

```js
// ininValue 값이 없는 경우
const res = [0, 1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array){
    console.log(`currentIndex : ${currentIndex}`);
    console.log(`accumulator : ${accumulator}`);
    console.log(`currentValue : ${currentValue}`);
    console.log(`array : ${array}`);
    console.log("                              ");
    return accumulator + currentValue;
});

console.log("res:", res);

//## [ reduce()함수 호출시 initialValue 값이 없는 경우 ]
//initialValue를 제공하지 않으면, reduce()는 인덱스 1부터 시작해
//  콜백 함수 실행하고 첫번째의 인덱스 값은 건너 뛰게된다.
// accumulator 는 배열의 첫번째 값
// currentValue 는 배열의 두번째 값
```

```js
// initValue 값이 있는 경우
var res = [0, 1, 2, 3, 4].reduce((accumulator, currentValue, currentIndex, array) => {
    console.log(`currentIndex : ${currentIndex}`);
    console.log(`accumulator : ${accumulator}`);
    console.log(`currentValue : ${currentValue}`);
    console.log(`array : ${array}`);
    console.log("                              ");
    return accumulator + currentValue;
}, 10);

console.log("res:", res);

//## [ reduce()함수 호출시 initialValue 값이 있는 경우 ]
// initialValue를 제공하면 인덱스 0에서 시작합니다.
// accumulator 는 initialValue
// currentValue 는 배열의 첫번째 값
```

```js
// 객체 배열에서의 값 합산
const initial = 0;
const lists = [
    {x : 1},
    {x : 2},
    {x : 3}
];
const sum = lists.reduce((acc, current) => {
    console.log(`accumulator : ${acc}`);
    console.log(`currentValue : ${current.x}`);
    console.log("                              ");   
    return acc + current.x;
}, initial)

console.log(sum) // logs 6
```

```js
// 중첩 배열 펼치기
const array = [
    [0, 1],
    [2, 3],
    [4, 5]
]
const sumArray = array.reduce((acc, current) => {
	console.log(`accumulator : ${acc}`);
        console.log(`currentValue : ${current}`);
        return acc.concat(current);
    }
,[]);

console.log(sumArray);
//[0, 1, 2, 3, 4, 5]
```

```js
// 배열의 중복 항목 제거

let arr = [1, 2, 1, 2, 3, 5, 4, 5, 3, 4, 4, 4, 4];
let result = arr.sort().reduce((accumulator, currentValue) => {
    console.log(`accumulator : ${accumulator}`);
    console.log(`currentValue : ${currentValue}`);
    console.log(`                              `);

    const length = accumulator.length
    if (length === 0 || accumulator[length - 1] !== currentValue) {
        accumulator.push(currentValue);
    }
    return accumulator;
}, []);
console.log(result); //[1,2,3,4,5]
```

