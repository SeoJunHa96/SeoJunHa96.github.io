---
title: Basic syntax of JavaScript
date: 2023-10-24 19:06:00 +09:00
categories: [JavaScript]
tags:
  [
    javascript,
    스코프,
    호이스팅,
    식별자,
  ]
---

# Basic syntax of JavaScript



- 식별자(변수명) 작성 규칙
  - 반드시 문자, 달러($), 밑줄(_)로 시작
  - 대소문자 구분
  - 예약어 사용 불가(for, if, function) 등
  - 카멜 케이스(camelCase) (가장 많이 씀) : 변수, 객체, 함수에 사용
  - 파스칼 케이스 : 클래스, 생성자에 사용
  - 대문자 스네이크 케이스(SNAKE_CASE) : 상수에 사용



- 변수 선언 키워드

  - let

    블록 스코프를 갖는 지역 변수를 선언

    재할당 가능

    재선언 불가능

    ES6에서 추가

    ```js
    let number = 10 // 1. 선언 및 초기값 할당
    number = 20 // 2. 재할당
    ---
    let number = 10 // 1. 선언 및 초기값 할당
    let number = 20 // 2. 재선언 불가능
    ```

    

  - const

    블록 스코프를 갖는 지역 변수

    재할당/재선언 불가능

    ES6에서 추가

    ```js
    const number = 10 // 1. 선언 및 초기값 할당
    number = 10 //2. 재할당 불가능
    const number = 20 // 3. 재선언 불가능
    
    ---
    const number // const` declarations must be initialized.
    // 선언 시 반드시 초기값 설정 필요
    ```



- 블록 스코프(block scope)

  if, for, 함수 등의 '중괄호({}) 내부'를 가리킴

  블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능

  작은 영역 쪽으로 찾는 것 불가능 (안에서 밖으로 찾는 건 가능)



- 변수 선언 키워드 정리
  - 기본적으로 const 사용을 권장
  - 재할당이 필요한 변수는 let으로 변경해서 사용



---

#### 데이터 타입

- 원시 자료형

  Number, String, Boolean, undefined, null

  변수에 값이 직접 저장되는 자료형(불변, 값이 복사)



- 참조 자료형

  Objects, Array, Function

  객체의 주소가 저장되는 자료형(가변, 주소가 복사)



- 원시 자료형 예시

  - 변수에 할당될 때 값이 복사됨
  - 변수 간에 서로 영향을 미치지 않음

  ```js
  const bar = 'bar'
  console.log(bar) // bar
  
  bar.toUpperCase()
  console.log(bar) // bar
  
  let a = 10
  let b = a
  b = 20
  console.log(a) // 10
  console.log(b) // 20
  ```

  

- 참조 자료형 예시

  - 객체를 생성하면 객체의 메모리 주소를 변수에 할당
  - 변수 간에 서로 영향을 미침

  ``` js
  const obj1 = {name: 'Alice', age: 30}
  const obj2 = obj1
  obj2.age = 40
  
  console.log(obj1.age) // 40
  console.log(obj2.age) // 40
  ```

  

- Number : 정수 또는 실수형 숫자를 표현하는 자료형

  ```js
  const a = 13
  const b = -5
  const c = 3.14 // float - 숫자 표현
  const d = 2.998e8 // 2.998 * 10^8 = 299,800,000
  const e = Infinity
  const f = -Infinity
  const g = NaN // Not a Number를 나타내는 값
  ```



- String

  텍스트 데이터를 표현하는 자료형

  '+'연산자를 사용해 문자열끼리 결합

  곱/나누기/뺄셈 불가능

  ```js
  const firstName = 'Tony'
  const lastName = 'Stark'
  const fullName = firstName + lastName
  
  console.log(fullName) // TonyStark
  ```



- 템플릿 리터널(Template literals)

  - 내장된 표현식을 허용하는 문자열 방식
  - 백틱을 이용하여 여러 줄에 걸쳐 문자열을 정의할 수 있고, 자바스크립트의 변수를 문자열 안에 바로 연결할 수 있음
  - 표현식은 '$'와 중괄호(${expression})로 표기
  - ES6+ 부터 지원

  ```js
  const age = 100
  const message = `홍길동은 ${age}세입니다.`
  console.log(message) // 홍길동은 100세입니다.
  ```



- null : 변수의 값이 없음을 의도적으로 표현할 때 사용 (명시적 부재)

  ```js
  let a = null
  console.log(a) // null
  ```

  

- undefined : 변수 선언 이후 직접 값을 할당하지 않으면 자동으로 할당됨 (암묵적 부재)

  ```js
  let b
  console.log(b) // undefined
  ```

  

- '값이 없음'에 대한 표현이 null과 undefined 2가지인 이유

  - JavaScript의 설계 실수가 아닌 초보자를 위한 배려(전공자가 아닌 사용자를 고려)
  - null이 원시 자료형 임에도 불구하고 object로 출력되는 이유는 JS설계 당시의 버그를 해결하지 않은 것
  - 해결하지 못하는 이유는 이미 null 타입에 의존성을 띄고 있는 수 많은 프로그램들이 망가질 수 있기 때문(하위 호환 유지)

  ```js
  typeof null // "object"
  typeof undefined // "undefined"
  ```

  

- Boolean (treu / false)

  조건문 또는 반복문에서 Boolean이 아닌 데이터 타입은 "자동 형변환 규칙"에 따라 true 또는 false로 변환됨



- 자동 형변환

  | 데이터 타입 |   false    |       true       |
  | :---------: | :--------: | :--------------: |
  |  undefined  | 항상 false |        X         |
  |    null     | 항상 false |        X         |
  |   Number    | 0, -0, NaN | 나머지 모든 경우 |
  |   String    | 빈 문자열  | 나머지 모든 경우 |



---

#### 연산자

- 할당 연산자

  오른쪽에 있는 피연산자의 평가 결과를 왼쪽 피연산자에 할당하는 연산자

  단축 연산자 지원

  ```js
  let a = 0
  
  a += 10 //10
  a -= 3 // 7
  a *= 10 // 70
  a %= 7 // 0
  ```

  

- 증가 & 감소 연산자

  - 증가 연산자 (++)

    피연산자를 증가시키고 연산자의 위치에 따라 증가하기 전이나 후의 값을 반환

  - 감소 연산자(--)

    피연산자를 감소시키고 연산자의 위치에 따라 감소하기 전이나 후의 값을 반환

  - += 또는 -=와 같이 더 명시적인 표현으로 작성하는 것을 권장

  ```js
  let x = 3
  const y = x++
  console.log(x, y) // 4 3
  let a = 3
  const b = ++a
  console.log(a, b) // 4 4
  ```



- 비교 연산자

  피연산자들(숫자, 문자, Boolean 등)을 비교하고 결과 값을 boolean으로 반환하는 연산자

  ```js
  3 > 2 //true
  3 < 2 // false
  'A' < 'B' // true
  'Z' > 'a' // true
  '가' < '나' // true
  ```



- 동등 연산자(==)

  두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환

  '암묵적 타입 변환'을 통해 타입을 일치시킨 후 같은 값인지 비교

  두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별

  ```js
  console.log(1 == 1) // true
  console.log('hello' == 'hello') // true
  console.log('1' == 1) // true
  console.log(0 == false) // true
  ```

   

- 일치 연산자(===)

  두 피연산자의 값과 타입이 모두 같은 경우 true를 반환

  같은 객체를 가리키거나, 같은 타입이면서 같은 값인지를 비교

  엄격한 비교가 이뤄지며 암묵적 타입 변환이 발생하지 않음

  특수한 경우(null과 undefined 비교)를 제외하고는 동등 연산자가 아닌 일치 연산자 사용 권장

  ```js
  console.log(1 === 1) // true
  console.log('hello' === 'hello') // true
  console.log('1' === 1) // false
  console.log(0 === false) // false
  ```



- 논리 연산자
  - and 연산 (&&)
  
  - or 연산 (||)
  
  - not 연산 (!)
  
  - 단축 평가 지원(단축 평가는 && 먼저, 그다음 ||)
  
  - ```
    단축 평가
    && -> 피연산자를 왼쪽에서 오른쪽으로 평가하면서 "첫" 거짓 같은 피연산자를 만나면, '즉시' 
    그 '값을 반환'한다, 만약 모든값이 참이면, 마지막을
    반환한다
    
    || -> 앞 피연산자를 true로 반환할 수 있으면
    앞 피연산자를 반환, 그렇지 않으면 뒤 피연산자 반환
    ```
  
    

---

#### 조건문

- if

  조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 판단

  ```html
  const name = 'customer'
  
  if (name === 'admin') {
  	console.log('관리자님 환영')
  } else if (name === 'customer'){
  	console.log('고객환영')
  } else {
  	console.log(`반갑습니다. ${name}님`)
  }
  ```



- 조건(삼항) 연산자

  세 개의 피연산자를 받는 유일한 연산자

  앞에서부터 조건문, 물음표, 조건문이 참일 경우 실행할 표현식, 콜론, 조건문이 거짓일 경울 실행할 표현식이 배치

  ```js
  const func1 = function(person){
      if(person > 17) {
          return 'Yes'
      } else {
          return 'No'
      }
  }
  ```

  ```js
  const func2 = function (person){
      return person > 17 ? 'Yes' : 'No'
  }
  
  /*
  조건문 / 물음표 / 참일 경우 실행 / 콜론 / 거짓일 경우 실행
  */
  ```



---

#### 반복문

while / for / for... in / for...of



- while

  조건문이 참이면 문장을 계속 수행

  ```js
  while (조건문) {
      // do something
  }
  ```

  ```js
  let i = 0
  while (i < 6){
      console.log(i)
      i += 1
  }
  ```

  

- for

  특정한 조건이 거짓으로 판별될 때까지 반복

  ```js
  for ([초기문]; [조건문]; [증감문]){
      // do something
  }
  ```

  ```js
  for (let i = 0; i<6; i++){
      console.log(i)
  }
  ```



- for ...in

  객체의 열거 가능한 속성(property)에 대해 반복

  ```js
  for (variable in object){
      statement
  }
  ```

  ```js
  const fruits = { a: 'apple', b: 'banana' };
  
  for (const property in fruits) {
      console.log(property); 
      console.log(fruits[property]);
  }
  /*
  a
  apple
  b
  banana
  */
  ```



- for ...of

  반복 가능한 객체(배열, 문자열 등)에 대해 반복

  ```js
  for (variable of iterable){
      statement
  }
  ```

  ```js
  const numbers = [0, 1, 2, 3]
  for(const number of numbers) {
      console.log(number)
  } // 0, 1, 2, 3
  ```



- 배열 반복과 for ...in

  - 배열의 인덱스는 정수 이름을 가진 열거 가능한 속성

  - for ...in은 정수가 아닌 이름과 속성을 포함하여 열거 가능한 모든 속성을 반환

  - 내부적으로 for ...in은 배열의 반복자 대신 속성 열거를 사용하기 때문에 특정 순서에 따라 인덱스를 반환하는 것을 보장할 수 없음

    :인덱스의 순서가 중요한 배열에서는 사용하지 않음

    배열에서는 for 반복, for ...of반복을 사용

  ```js
  const arr = ['a', 'b', 'c']
  
  for (const i in arr) {
      console.log(i) 
  } // 0, 1, 2
  for (const i of arr) {
      console.log(i)
  } // a, b, c
  ```

  

- for ...in 과 for ...of 비교

  ```js
  //for ...in
  
  // Array
  const arr = ['a', 'b', 'c']
  for (const elem in arr){
      console.log(elem) 
  } // 0 1 2
  
  // Object
  const capitals = {
      korea : '서울',
      japan : '도쿄',
      china : '베이징',
  }
  for (const capital in capitals){
      console.log(capital)
  } // korea japan china
  ```

  ```js
  //for ...of
  
  // Array
  const arr = ['a', 'b', 'c']
  for (const elem of arr){
      console.log(elem) 
  } // a b c
  
  // Object
  const capitals = {
      korea : '서울',
      japan : '도쿄',
      china : '베이징',
  }
  for (const capital of capitals){
      console.log(capital)
  } // TypeError: capitals is nor iterable
  ```



- 반복문 사용 시 const 사용 여부

  - for 문

    ```js
    for (let i = 0; i<arr.length; i++) {...} 의 경우에는
    최초 정의한 i를 "재할당"하면서 사용하기 때문에
    const 사용시 에러 발생
    ```

  - for...in, for...of

    ```js
    재할당이 아니라, 매 반복마다 다른 속성 이름이 변수에 지정되는 것이므로
    const를 사용해도 에러 발생하지 않음
    단, const특징에 따라 블록 내부에서 변수를 수정할 수 없음
    ```



- 반복문 종합

  |   키워드   |   연관 키워드   |   스코프    |
  | :--------: | :-------------: | :---------: |
  |   while    | break, continue | 블록 스코프 |
  |    for     | break, continue | 블록 스코프 |
  | for ... in |   object 순회   | 블록 스코프 |
  | for ... of |  Iterable 순회  | 블록 스코프 |

  

---

#### 참고

- 세미콜론
  - 자바스크립트는 세미콜론을 선택적으로 사용 가능
  - 세미콜론이 없으면 ASI에 의해 자동으로 세미콜론이 삽입됨
  - ASI : Automatic Semicolon Insertion, 자동 세미콜론 삽입 규칙
  - JS를 만든 Brendan Eich  또한 세미콜론 작성을 반대



- 변수 선언 키워드 var
  - ES6 이전에 변수 선언에 사용했던 키워드
  - 재할당, 재선언 가능
  - 호이스팅 되는 특성으로 인해 예기치 못한 문제 발생 가능
  - 따라서 var 대신 const와 let을 사용하는 것을 권장
  - 함수 스코프를 가짐
  - 변수 선언 시 var, const, let 키워드 중 하나를 사용하지 않으면 자동으로 var로 선언됨



- 함수 스코프(function scope)

  함수의 중괄호 내부를 가리킴

  함수 스코프를 가지는 변수는 함수 바깥에서 접근 불가능

  ```js
  function foo(){
      var x = 1
      console.log(x) // 1
  }
  console.log(x) // ReferenceError : x is not defined
  ```



- 호이스팅

  런타임 이전에, "선언문"들이 끌어올려지는 행위

  변수 선언 이전에 참조할 수 있는 현상

  변수 선언 이전의 위치에서 접근 시 undefined를 반환
  
  ```js
  console.log(name) // undefined : 선언 이전에 참조
  var name = '홍길동' // 선언
  ```
  
  ```js
  // 위 코드를 암묵적으로 아래와 같이 이해항
  var name
  console.log(name)
  var name = '홍길동'
  ```


  JS에서 변수들은 실제 실행시에 코드의 최상단으로 끌어 올려지게 되며(hoisted)

  이러한 이유 때문에 var로 선언된 변수는 선언 시에 undefined로 값이 초기화되는 과정이 동시에 발생

  ```js
  console.log(name) // undefined
  var name = '홍길동'
  
  console.log(age) // ReferenceError: Cannot access 'age' before initialization
  let age = 30
  
  console.log(height) // ReferenceError: Cannot access 'height' before initialization
  const height = 180
  ```

  

- NaN을 반환하는 경우 예시

  - 숫자로서 읽을 수 없음(Number(undefined))
  - 결과가 허수인 수학 계산식 (Math.sqrt(-1))
  - 피연산자가 NaN(7**NaN)
  - 정의할 수 없는 계산식(0*Infinity)
  - 문자열을 포함하면서 덧셈이 아닌 계산식('가'/3)

  ```js
  const Joke = 'ba' + + 'a' + 'a'
  console.log(Joke.toLowerCase())
  // banana
  ```

  

- 실습 5번 문제

  ```js
  const citiesInfo = [
    {
      city: '서울',
      utcOffset: ['한국 표준시', 'KST', 'UTC+9'],
      latitude: 37,
      longitude: 126
    },
    {
      city: '도쿄',
      utcOffset: ['일본 표준시', 'JST', 'UTC+9'],
      latitude: 35,
      longitude: 139
    },
    {
      city: '상하이',
      utcOffset: ['중국 표준시', 'CST', 'UTC+8'],
      latitude: 31,
      longitude: 121
    }
  ];
  
  for (var i = 0; i < citiesInfo.length; i++) {
    for (const key in citiesInfo[i]) {
      if (key === 'city') {
        console.log('수도 : ' + citiesInfo[i][key]);
      } else {
        if (Array.isArray(citiesInfo[i][key])) {
          console.log(key + ' : ' + citiesInfo[i][key][citiesInfo[i][key].length - 1]);
        } else {
          console.log(key + ' : ' + citiesInfo[i][key]);
        }
      }
    }
    console.log('');
  }
  
  ```

  


- var의 단점(VS let, const)

  함수 레벨 스코프 

  var 키워드 생략 허용 

  변수 중복 선언 허용(재 선언) 

  변수 호이스팅 발생 

  긴 생명주기 (메모리 낭비)

  암묵적 결합 

  스코프 체인 상 종점에 위치 

  네임스페이스 오염



- 프론트엔드 영역에서 많이 쓰는 단축 평가

  ```html
  {data && <div> {data} </div>}
  data에 값이 있을 경우 data가 출력 된다.
  ```

  