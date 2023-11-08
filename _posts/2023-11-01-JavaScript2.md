---
title: JavaScript 2
date: 2023-11-03 19:06:00 +09:00
categories: [JavaScript]
tags:
  [
    JavaScript,
  ]
---

# JavaScript 2(ver. 코딩앙마)

---

#### 변수

- const

  

- var : 한 번 선언된 변수를 다시 선언할 수 있다.

  ​		선언하기 전에 사용할 수 있다.(호이스팅)

  ​		선언은 호이스팅 되지만, 할당은 호이스팅 되지 않음.(undefined)

  ```js
  var name = 'Mike';
  console.log(name);  // Mike
  
  var name = 'Jane';
  console.log(name); // Jane
  ```

- let : 다시 선언하면 에러 발생



- 호이스팅

  스코프 내부 어디서든 변수 선언은 최상위에 선언된 것 처럼 행동

  변수명은 호이스팅 되지만 할당은 호이스팅 되지 않는다. 



- 변수 생성 과정

  - 선언, 초기화, 할당의 단계를 거침 

  -  var는 선언과 초기화(undefined를 할당)가 동시에, 할당 전에 호출해도 에러가 발생하지 않음

  - let은 선언과 초기화가 분리, 호이스팅되며 선언이 이루어지지만, 초기화는 실제 코드에 도달했을 때 실행되기 때문에 에러 발생

  - const는 선언, 초기화, 할당이 동시에 실행. 

    ```js
    const gender;
    gender = 'male';
    // 에러가 발생한다.
    
    const gender = 'male';
    ```



- 가급적 let과 const를 사용, 에러를 줄일 수 있다.

---

#### 생성자 함수

- 객체 리터럴

  ```js
  let user = {
      name : 'Mike',
      age : 30,
  }
  ```



- 생성자 함수(회원, 상품 등 비슷한 객체를 여러개 만들 때 사용)

  ```js
  function User(name, age){ //첫 글자 대문자
      this.name = name;
      this.age = age;
  }
  
  let user1 = new User('Mike', 30);  // new 연산자를 사용해서 호출
  let user2 = new User('Jane', 22);
  let user3 = new User('Tom', 17);
  ```



- 예시

  ```js
  // 상품 생성
  function Item(title, price){
      //this = {}; 실제로 작성되진 않지만, new를 사용하게 되면 이 코드가 실행된다.
      
      this.title = title;
      this.price = price;
      this.showPrice = functions(){
          console.log('가격은 ${price}원 입니다.');
      };
      //return this;
  }
  
  const item1 = new Item("인형", 3000);
  const item2 = new Item("가방", 4000);
  const item3 = new Item("지갑", 5000);
  
  item3.showPrice();
  // 가격은 5000원 입니다.
  ```

  

- 생성자 함수는 반드시 new를 붙여서 사용해야 한다.



---

#### Intermediate Class

- Computed property (계산된 프로퍼티)

  ```js
  let a = 'age';
  const user = {
      name : 'Mike',
      age : 30, // age 대신 [a]를 사용 가능
  }
  
  ```

  ```
  const user = {
  	[1+4] :5,
  	["안녕" + "하세요"] : "Hello"
  }
  
  user
  > {5:5, 안녕하세요: "Hello"}
  ```

  

- Methods

  - Object.assign() : 객체 복제

    ```js
    const user = {
        name : 'Mike',
        age : 30
    }
    
    const newUser = Object.assign({}, user);
    // 빈 객체는 초기값, 두번째 이후 변수들이 초기값에 병합된다.
    
    newUser != user //복제를 해도 같은 객체는 아님.
    // 초기값이 꼭 비어있을 필요는 없음.
    // 초기값에 키가 같은 것이 있다면 덮어씀.
    // 두 개 이상도 덮어쓸 수 있음.
    ```

    

  - Object.keys() : 키 배열 반환

    ```js
    const user = {
        name : 'Mike',
        age : 30,
        gender : 'male',
    }
    
    Object.keys(user);
    //["name", "age", "gender"]
    ```

    

  - Object.values() : 값 배열 반환

    ```js
    const user = {
        name : 'Mike',
        age : 30,
        gender : 'male',
    }
    
    Object.values(user);
    //["Mike", 30, "male"]
    ```

    

  - Object.entries() : 키/값 배열 반환

    ```js
    const user = {
        name : 'Mike',
        age : 30,
        gender : 'male',
    }
    
    Object.entries(user);
    // [["name", "Mike"], ["age", 30], ["gender", "male"]]
    ```

    

  - Object.fromEntries() : 키/값 배열을 객체로

    ```js
    const arr = [["name", "Mike"], ["age", 30], ["gender", "male"]];
    
    Object.fromEntries(arr);
    /*
    const user = {
        name : 'Mike',
        age : 30,
        gender : 'male',
    }
    */
    ```




---

#### 심볼(Symbol)_자료형

- 기본 형태

  ```js
  // 유일한 식별자를 만들 때 사용한다.
  const a = Symbol(); // new를 붙이지 않는다.
  const b = Symbol();
  
  console.log(a) // Symbol()
  console.log(b) // Symbol()
  
  a == b;
  false
  a === b;
  false
  ```



- 유일성 보장

  ```js
  const id = Symbol('id');  // 설명을 붙일 수 있음
  const id2 = Symbol('id');
  
  id // Symbol(id)
  id2 // Symbol(id)
  id === id2 //false
  id == id2 //false
  ```

  

- property key : 심볼형

  ```js
  const id = Symbol('id');
  const user = {
      name : 'Mike',
      age : 30,
      [id] : 'myid'
  }
  user
  //{name : "Mike", age: 30, Symbol(id):"myid"}
  
  Object.keys(user); //["name", "age"]
  // 심볼형인 것들은 key, values, entries, for 등이 건너 뜀
  ```

  

- 특정 개체의 원본 데이터는 건드리지 않고,  속성 추가 가능

  ```js
  coonst user = {
      name : "Mike",
      age : 30,
  }
  const id = Symbol('id');
  user[id] = 'myid';
  ```



- 전역 심볼(Symbol.for())

  - 하나의 심볼만 보장받을 수 있음
  - 없으면 만들고, 있으면 가져오기 때문
  - Symbol 함수는 매번 다른 Symbol 값을 생성하지만, 
  - Symbol.for 메소드는 하나를 생성한 뒤 키를 통해 같은 Symbol을 공유

  ```js
  const id1 = Symbol.for('id');
  const id2 = Symbol.for('id');
  
  id1 === id2; //true
  
  Symfol.keyFor(id1) // "id"
  ```



- description

  ```js
  const id = Symbol('id');
  
  const user = {
      name : 'Mike',
      age : 30,
      [id] : 'myid'
  }
  
  Object.getOwnPropertySymbols(user); //[Symbol(id)]
  
  Reflect.ownKeys(user); ["name", "age", Symbol(id)]
  ```

  

- 활용

  ```js
  // 다른 사람이 만든 객체
  const user = {
      name : "Mike",
      age : 30,
  };
  
  // 내가 직접 함수를 추가할 때 (다른 사람이 만든 객체는 건드리지 않고)
  const showName = Symbol("show name");
  user[showName] = funciont(){
      console.log(this.name)
  };
  
  user[showName](); //Mike
  
  //사용자가 접속하면 보는 메세지
  for (let key in user) {
      console.log('His ${key} is ${user[key]}.');
  }
  ```



---

#### Number, Math

- toString()

  10진수 -> 2진수/16진수

  ```js
  let num = 10;
  num.toString(); //"10"
  num.toString(2); // "1010"
  
  let num2 = 255;
  num2.toString(16); //"ff" 255의 16진수 표현
  ```



- Math

  ``` js
  Math.Pi; //3.141592653589793
  ```

  

- 올림

  ```js
  Math.ceil() // 올림
  
  let num = 5.1;
  Matt.ceil(num); // 6 
  ```

  

- 내림

  ```js
  Math.floor() 
  ```



- 반올림

  ```js
  Math.round()
  
  // 소수점 자리수 표현
  let userRate = 30.1234;
  Math.round(userRate * 100)/100 //30.12
  ```

  

- 소수점 자릿수

  ```js
  toFixed()
  let userRate = 30.1234;
  userRate.toFixed(2) //"30.12 "
  
  // 주의사항 : 문자열 반환임
  // Number(userRate.toFixed(2)); 그래서 이런식으로 많이 함
  ```

  

-  NAN

  ```js
  isNaN()
  //NaN 은 잘못된 입력으로 인해 계산할 수 없음을 나타내는 기호
  let x = Number('x'); //NaN
  
  x == NaN	// false
  x === NaN	// false
  NaN == NaN	// fasle
  
  isNaN(x) // true
  isNaN(3) // false
  ```

  

- parseInt()

  ```js
  let margin = '10px';
  // 문자를 숫자로 바꿔줌, Number와 다른 점은 문자와 혼용되있어도 가능
  
  parseInt(margin); // 10
  Number(margin);   //NaN
  
  
  let reColor = 'f3';
  parseInt(redColor); //NaN
  
  parseInt(redColor, 16); // 243
  
  parseInt('11', 2) // 3
  ```



- parseFlot()

  ```js
  let padding = '18.5%';
  parseInt(padding); // 18
  parseFloat(padding); // 18.5
  
  // 부동소숫점 반환
  ```

  

- 랜덤 숫자

  ```js
  Math.random()
  0~1 사이 무작위 숫자 생성
  
  // 1~100 사이 임의의 숫자?
  Math.floor(Math.random()*100)+1
  ```



- 최대, 최소

  ```js
  Math.max()/Math.min()
   
  // 괄호 안의 인수들 중 최대/최소값 구함.(음수, 실수도 가능)
  
  ```



- 절대값

  ```js
  Math.abs():
  ```



- 제곱

  ```js
  Math.pow(n, m)
  // n의 m승 값
  ```



- 제곱근

  ```js
  Math.sqrt()
  ```

  

----

#### String

- 백틱(`)여러줄 포함가능

  ```js
  let desc = `오늘은 맑고 화창한
  날씨가 계속 됨
  내일 비.`;
  
  // 일반 따옴표로 하려면 \n을 써야한다.
  ```



- 문자열 길이

  ```js
  let desc = '안녕하세요.';
  desc.length // 6
  ```



- 특정 위치 접근

  ```js
  let desc = '안녕하세요.';
  desc[2] //'하'
  ```

  - 배열과 다르게 한글자만 바꾸는 것은 허용되지 않는다. (변화없음)



- 대/소문자

  ```js
  toUpperCase()/toLowerCase()
  
  // 전부 대문자로 / 전부 소문자로
  ```

  

- 문자를 인수로 받아 인덱스 반환

  ```js
  str.indexOf(text)
  let desc = "Hi guys. Nice to meet you.";
  
  desc.indexOf('to'); // 14, t가 시작하는 인덱스 번호 14
  desc.indexOf('man'); // -1, 찾는게 없으면 -1 반환
  ```

  

- 슬라이스

  ```js
  str.slice(n, m)
  // n은 시작점
  // m은 없으면 문자열 끝까지, 양수면 그 숫자까지(포함하진 않음), 음수면 끝에서부터 센다.
  
  let desc = "abcdefg";
  desc.slice(2) //"cdefg"
  desc.slice(0, 5) // "abcde"
  desc.slice(2, -2) // "cde", 2부터 끝에서 2까지
  
  
  ```

  

- 사이 문자 반환

  ```js
  str.substring(n, m)
  // n과 m사이 문자열 반환
  // 음수 허용하지 않음, 음수는 0으로 인식
  let desc = "abcdefg";
  desc.substring(2, 5); // "cde"
  desc.substring(5, 2); // "cde"
  ```



- 사이문자 반환2

  ```js
  str.substr(n, m)
  // n부터 시작, m개
  let desc = "abcdefg";
  desc.substr(2, 4)  //"cdef"
  desc.substr(-4, 2) // "de"
  ```



- 앞 뒤 공백 제거

  ```js
  str.trim()
  ```



- 반복

  ```js
  str.repeat(n)
  //n번 반복
  ```

  

- 비교

  ```js
  "a" < "c" // true
  
  // 문자열을 숫자로 얻는 방법
  "a".codePointAt(0); //97, 아스키 코드
  String.fromCodePoint(97) // a
  ```

  

---

#### Array

- 기초
  - push() : 뒤에 삽입
  - pop() : 뒤에 삭제
  - unshift() : 앞에 삽입
  - shift() : 앞에 삭제



- 특정 요소 지움

  ```js
  arr.splice(n, m)
  // n에서 시작, m개 지움
  
  let arr = [1, 2, 3, 4, 5];
  arr.splice(1, 2);
  
  console.log(arr); //[1, 4, 5]
  ```

  ```js
  arr.splice(n, m, x)
  // 특정 요소 추가
  
  let arr = [1, 2, 3, 4, 5];
  arr.splice(1, 3, 100, 200)
  console.log(arr); // [1, 100, 200, 5]
  
  let arr = ["나는", "철수", "입니다"];
  arr.splice(1, 0, "대한민국", "소방관");
  console.log(arr); // ["나는", "대한민국", "소방관", "철수", "입니다"]
  ```

  ```js
  arr.splice(): 
  // 삭제된 요소 반환
  
  let arr = [1, 2, 3, 4, 5];
  let reuslt = arr.splice(1, 2);
  
  console.log(arr); //[1, 4, 5]
  console.log(result); //[2, 3]
  ```



- slice

  ```js
  arr.slice(n, m)
  // n부터 m까지 반환
  
  let arr = [1, 2, 3, 4, 5];
  arr.slice(1, 4); // [2, 3, 4]
  ```

  

- concat

  ```js
  arr.concat(arr2, arr3 ...)
  // 합쳐서 새 배열 반환
  let arr = [1, 2];
  arr.concat([3, 4]); // [1, 2, 3, 4]
  arr.concat([3, 4], 5, 6); // [1, 2, 3, 4, 5, 6]
  ```

  

- indexOf / lastIndexOf

  ```js
  // 발견하면 해당 요소의 인덱스 반환, 없으면 -1 반환
  arr.indexOf / arr.lastIndexOf
  
  let arr = [1, 2, 3, 4, 5, 1, 2, 3];
  arr.indexOf(3); //2
  arr.indexOf(3, 3) // 7
  // 두번째 인수는 탐색 시작 위치
  
  arr.lastIndexOf(3); // 7 끝에서부터 탐색
  ```

  

- includes() : 포함 여부

  ```js
  let arr = [1, 2, 3];
  arr.includes(2); // true
  arr.includes(8); // flase
  ```



- find(fn), findIndex(fn) : indexof와 같지만 함수를 넣어 복잡한 연산 가능

  ```js
  // 첫 번째 true 값만 반환하고 끝, 없으면 undefined 반환
   
  let arr = [1, 2, 3, 4, 5];
  
  const result = arr.find((item)=>{
      return item % 2 === 0;
  });
  
  console.log(result);
  //2
  ```

  ```js
  let userList = [
      { name: "Mike", age:30 },
      { name: "Jane", age:27 },
      { name: "Tom", age:10 },
  ];
  
  const result = userList.find((user)=>{
      if (user.age < 19){
          return true;
      }
      return false;
  });
  
  console.log(result);
  //{name: "Tom", age: 10}
  
  //findeIndex로 하면 2가 출력된다.
  ```

  

- filter(fn)

  ```js
  // 만족하는 모든 요소를 배열로 반환
  
  const arr = [1, 2, 3, 4, 5, 6];
  
  const result = arr.filter((item)=>{
      return item % 2 === 0;
  });
  
  console.log(result);
  // [2, 4, 6]
  ```

  

- reverse()

  ```js
  // 역순으로 재정렬
  let arr = [1, 2, 3, 4, 5];
  arr.reverse();
  //[5, 4, 3, 2, 1]
  ```

  

- map

  ```js
  // 함수를 받아 특정 기능을 시행하고, 새로운 배열을 반환
  let userList = [
      { name: "Mike", age:30 },
      { name: "Jane", age:27 },
      { name: "Tom", age:10 },
  ];
  
  let newUserList = userList.map((user, index) => {
      return Object.assign({}, user, {
          id : index+1,
          isAdult:user.age > 19,
      });
  });
  
  console.log(newUserList);
  //
  {"name": "Mike", "age": 30, "id": 1, "isAdult": true},
  {"name": "Jane", "age": 27,"id": 2, "isAdult": true},
  {"name": "Tom", "age": 10, "id": 3, "isAdult": false}
  
  ```



- join

  ```js
  let arr = ["안녕", "나는",  "철수야"];
  
  let result = arr.join();
  console.log(result);
  // 안녕, 나는, 철수야 (기본적으로 ,로 연결 / 아니면 조인 안의 요소로 연결)
  let result = arr.join(-);
  console.log(result);
  // 안녕-나는-철수야
  ```



- split

  ```js
  // 잘라서 배열로 만들어줌
  const users = "Mike, Jane, Tom, Tony"
  const result = user.split(",");
  console.log(result);
  //["Mike", "Jane", "Tom", "Tony"]
  ```

  

- Array.isArray()

  ```js
  // 배열인지 아닌지 확인
  let user = {
      name: "Mike",
      age: 30,
  };
  
  let userList = ["Mike", "Tom", "Jane"];
  
  console.log(Arry.isArry(user));		// false
  console.log(Arry.isArry(userList));	// treu
  ```



---

#### 배열 메소드2 (sort, reduce)

- sort()

  ```js
  // 배열 재정렬, 배열 자체가 변경되니 주의
  
  let arr = [1, 5, 4, 2, 3];
  arr.sort();
  console.log(arr);
  // [1, 2, 3, 4 ,5]
  // 문자열(알파벳) 가능
  
  // 문자열로 취급하기 때문에
  let arr = [27, 8, 5, 13];
  arr.sort();
  console.log(arr);
  // [13, 27, 5, 8] 이라는 결과가 출력된다.
  
  // 따라서 정렬을 위해서 인수로 정렬 로직을 담은 함수를 받아야 한다.
  let arr = [27, 8, 5, 13];
  function fn(a, b) {
      return a - b;
  }
  arr.sort(fn);
  console.log(arr);
  //[5, 8, 13, 27]
  
  // 혹은
  arr.sort((a, b) => {
      return a - b;
  });
  // 해도 결과는 동일
  ```

  ```js
  // 헷갈리고 어렵기 때문에
  // Lodash라는 라이브러리를 사용
  _.sortBy(arr);
  
  https://lodash.com/
  ```



- reduce

  ```js
  /**
  arr.reduce()
  인수로 함수를 받음
  (누적 계산값, 현재값) => (return 계산값);
  **/
  ```

  ```js
  // 배열의 모든 수 합치기
  let arr = [1, 2, 3, 4, 5];
  
  // forEach
  let result = 0;
  arr.forEach((num) => {
      result += num;
  });
  
  console.log(result) // 15
  
  // reduce
  
  const result = arr.reduce((prev, cur)=>{
      return prev + cur;    
  }, 0) // 초기값 0
  console.log(result); //15
  ```

---

#### 구조 분해 할당 (Destructuring assignment)

- 배열 구조 분해

  ```js
  let [x, y] = [1, 2];
  
  console.log(x); //1
  console.log(y); //2
  
  let users = ['Mike', 'Tom', 'Jame'];
  let [user1, user2, user3] = users;
  // let user2 = users[1];
  
  console.log(user2); //'Tom'
  ```

  ```js
  let [a, b, c] = [1, 2];
  // c는 undefined가 된다.
   
  let[a= 3, b= 4, c=5] = [1, 2];
  // 기본값 설정
  // a, b 는 1, 2가 되고, c는 기본값이었던 5가 된다.
  ```

  ```js
  // 공백을 통해 필요없는 값 무시 가능
  let [user1, , user2] = ['Mike', 'Tom', 'Jane', 'Tony'];
  console.log(user1); // 'Mike'
  console.log(user2); // 'Jane'
  ```

- 바꿔치기

  ```js
  let a = 1;
  let b = 2;
  
  let c = a;
  a = b;
  b = c;
  
  // 구조분해 할당
  [a, b] = [b, a];
  ```



- 객체 구조 분해

  ```js
  let user = {name: 'Mike', age: 30};
  let {name, age} = user;
  console.log(name); //'Mike'
  console.log(age); //30
  ```

  ```js
  // 객체 구조 분해 : 새로운 변수 이름으로 할당
  let user = {name:'Mike', age: 30};
  let {name, age} = user;
  let {name : userName, age : userAge} = user;
  console.log(userName); // 'Mike'
  console.log(userAge); // 30
  ```



- 객체 구조 분해, 기본값

  ```js
  let user = {name: 'Mike', age:30};
  let {name, age, gender} = user;
  
  gender = undefined
  
  let {name, age, gender = 'male'} = user;
  ```

  

---

#### 나머지 매개변수, 전개 구문

```js
function showName(name){
    console.log(name);
}

showName('Mike', 'Tom');
// 에러는 발생하지 않고 Mike만 출력
showNmae();
// undefined
```



- js에서 인수에 넘겨주는 개수에는 제한이 없다.



- arguments

  - 화살표 함수에서 사용불가
  - 함수로 넘어 온 모든 인수에 접근
  - 함수내에서 이용 가능한 지역 변수
  - length/index
  - Array 형태이 객체
  - 배열의 내장 메서드 없음

  ```js
  function showName(name){
      console.log(arguments.length);
      console.log(arguments.[0]);
      console.log(arguments.[1]);
  }
  
  showName('Mike', 'Tom');
  // 2
  // 'Mike'
  // 'Tom'
  ```

  

- 나머지 매개변수(Rest parameters)

  정해지지 않은 개수의 인수를 배열로 나타낼 수 있게 한다.

  ```js
  function showName(...names){
      console.log(names);
  }
  showName(); // []
  showName('Mike'); // ['Mike']
  showName('Mike', 'Tom'); // ['Mike', 'Tom']
  ```

  ```js
  function add(...numbers){
      let result = 0;
      numbers.forEach((num)=> (result += num));
      console.log(result);
  }
  
  add(1, 2, 3); // 6
  ```

  

  - 나머지 매개변수를 이용한 user 객체를 만드는 생성자 함수

  ```js
  // 나머지 매개변수는 항상 마지막에 입력
  function User(name, age, ...skills){
      this.name = name;
      this.age = age;
      this.skills = skills;
  }
  
  const user1 = new User('Mike', 30, 'html', 'css');
  console.log(user1) // User{name:'Mike', age: 30, skills: Array(2)}
  ```

  

- 전개 구문(Spread syntax) : 배열

  ```js
  let arr1 = [1, 2, 3];
  let arr2 = [4, 5, 6];
  
  let result = [...arr1, ...arr2];
  // ...arr1은 arr1을 풀어서 쓴 것.
  
  console.log(result); //[1, 2, 3, 4, 5, 6]
  
  let resuet = [0, ...arr1, ...arr2, 7, 8]
  // 중간에 쓰는 것도 가능함
  ```

  - 객체도 가능

  ```js
  let user = {name:'Mike'}
  let mike = {...user, age:30}
  
  console.log(mike) // {name:"Mike", age:30}
  ```

  - 전개 구문 : 복제(별개의 변수로 복제)

  ```js
  let arr = [1, 2, 3];
  let arr2 = [...arr]; //[1, 2, 3]
  
  let user = {name:'Mike', age:30};
  let user2 = {...user};
  
  user2.name = "Tom";
  
  console.log(user.name); // "Mike"
  console.log(user2.name); // "Tom"
  ```

  

  ```js
  let arr1 = [1, 2, 3];
  let arr2 = [4, 5, 6];
  
  arr1 = [...arr2, arr1];
  console.log(arr1); //[4, 5, 6, 1, 2, 3]
  ```

  ```js
  let user = {name : "Mike"};
  let info = {age : 30};
  let fe = ["JS", "React"];
  let lang = ["Korean", "English"];
  
  
  user = {
      ...user,
      ...info,
      skills: [
          ...fe,
          ...lang,
      ]
  }
  console.log(user)
  /*
  [object Object] {
    age: 30,
    name: "Mike",
    skills: ["JS", "React", "Korean", "English"]
  }
  */
  ```

  

---

#### 클로저(Closure)

- 어휘적 환경 

  전역 Lexical환경, 내부 Lexical환경이 존재

  변수, 함수명은 호이스팅되어 전역 Lexical 환경에 저장

  함수 내부의 변수는 내부 Lexical환경에 저장된다.

  내부 Lexical 환경은 전역 Lexical환경을 참조한다. 

  함수 안의 변수들은 내부 Lexical 환경에서 먼저 찾고 없으면, 전역 Lexical 환경에서 탐색한다.



- 클로저

  함수와 렉시컬 환경의 조합

  함수가 생성될 당시의 외부 변수를 기억

  생성 이후에도 계속 접근 가능

```js
function makeAdder(x){
    return function(y){
        return x+y;
    }
}

const add3 = makeAdder(3);

console.log(add3);  // function(y){return x+y;}
console.log(add3(2)); // 5
```

```js
function makeCounter() {
    let num = 0;
    
    return function () {
        return num++;
    };
}

let counter = makeCounter();

console.log(counter()); //0
console.log(counter()); //1
console.log(counter()); //2
```



---

#### setTimeout / setInterval

일정 시간이 지난 후 함수 실행 / 일정 시간 간격으로 함수 반복



- setTimeout

  ```js
  // 3초 뒤 3을 출력
  function fn(){
      console.log(3)
  }
  setTimeout(fn, 3000);
  // setTimeout은 2개의 매개변수를 받음
  // 1. 일정 시간이 지난 뒤 실행할 함수
  // 2. 시간(3000 = 3s)
  
  setTimeout(function(){
      console.log(3)
  }, 3000);
  ```

  ```js
  // 인수가 필요하다면 시간 뒤에 적어줌
  function showNmae(name){
      console.log(name);
  }
  
  setTimeout(showName, 3000, 'Mike');
  
  
  const tId = function showNmae(name){
      			console.log(name);
  			}
  			setTimeout(showName, 3000, 'Mike');
  
  cleatTimeout(tId);
  // 예정된 작업을 삭제
  ```

  

- setInterval

  ```js
  function showNmae(name){
      console.log(name);
  }
  const tId = setInterval(showName, 3000, 'Mike');
  // 반복 실행
  
  clearInterval(tId); // 실행 중지
  ```



- delay

  delay타임을 0으로 해도 바로 실행되지는 않는다.

  ```js
  setTimeout(function(){
      console.log(2)
  }, 0);
  
  console.log(1);
  // 1 
  // 2
  
  // 대기시간을 0으로 해도 1이 먼저 출력되고 그 뒤에 2가 출력된다.
  ```

  - 이유는 스크립트가 종료된 이후 스케쥴링 함수를 실행하기 때문
  - 또한 브라우저는 기본적으로 4ms 정도의 대기시간이 있다. 

  ```js
  let num = 1;
  
  function showTime() {
    //글은 백틱으로 작성, 변수는${}로 입력
    console.log(`접속하신지 ${num++}초가 지났습니다.`); 
    if (num>5){
      clearInterval(tId); 
    }
  }
  
  const tId = setInterval(showTime, 1000);
  ```

  

---

#### call, apply, bind

함수 호출 방식과 관계 없이 this를 지정할 수 있음

```js
// call 메서드는 모든 함수에서 사용할 수 있으며, this를 특정값으로 지정할 수 있다.
const mike = {
    name:"mike",
};

const tom = {
    name:"Tom",
};

function showThisName(){
    console.log(this.name);
}

showThisName(); //
showThisName.call(mike); //Mike
showThisName.call(tom); //Tom
```

```js
// apply는 함수 매개변수를 처리하는 방법을 제외하면 call과 같다.
// apply는 매개변수를 배열로 받는다.

const num = [3, 10, 1, 6, 4];
const minNum = Math.min(...num); // 1

const minNum = Math.min.apply(null, nums); // 1
// 하나씩 돌아가면서 인수로 사용한다.

const maxNum = Math.max.call(null, ...nums); //10
```

```js
// bind는 함수의 this값을 영구히 바꿀 수 있다.

const mike = {
    name: 'Mike',
};

function update(birthYear, occupation){
    this.birthYear = birthYear;
    this.occupation = occupation;
}

const updateMike = update.bind(mike);

updateMike(1980, "police");
console.log(mike);
/*
{
  birthYear: 1980,
  name: "Mike",
  occupation: "police"
}
*/
```

```js
const user = {
    name:"Mike",
    showName:function() {
        console.log(`hello, ${this.name}`);
    },
};
user.showName(); //"hello, Mike"

let fn = user.showName;
fn(); //hello,
// fn을 할당할 때 this를 잃어버린 것.

fn.call(uesr); //"hello, Mike"
fn.apply(user); //"hello, Mike"

let boundFn = fn.bind(user);
boundFn(); // "hello, Mike"
```



---

#### 상속, prototype

```js
// 공통된 부분 처리
 
const car = {
    wheels : 4,
    drive() {
        console.log("drive..");
    },
};


const bmw = {
    color: "red",
    navigation: 1,
};

const benz = {
    color: "black",
};

const audi = {
    color: "blue",
};

bmw.__proto__ = car;
benz.__proto__ = car;
audi.__proto__ = car;
// car 가 bmw의 프로토타입이 되는 것.
// bmw는 car의 상속을 받는 것.

console.log(bmw) // bmw 객체 출력
console.log(bmw.wheels) // 4 	


// Prototype Chain(프로토타입 체인)
const x5 = {
    color:"white",
    name: "x5",
};

x5.__proto__ = bmw;

console.log(x5.navigation) //1

// x5는 bmw를 상속 받고, bmw는 car를 상속 받기 때문에
// 거슬러 올라가서 x5가 car의 drive()를 상속 받을 수 있다.
```



```js
const Bmw = function (color){
    this.color = color;
};

Bmw.prototype.wheels = 4;
Bmw.prototype.drive = function(){
    console.log("dirve..");
};

const x5 = new Bmw("red");
const x4 = new Bmw("blue");
// .__proto__ 과정의 중복 코드 줄이기
```



---

#### Class

```js
const User = function (name, age) {
    this.name = name;
    this.age = age;
    this.showName = function() {
        console.log(this.name);
    };
};

const mike = new User("Mike", 30);

class User2 {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
    showName(){
        console.log(this.name)
    }
}

const tom = new User2('Tom', 19);

console.log(tom) 
/* {
  age: 19,
  name: "Tom"
}
*/

console.log(mike)
/*
{
  age: 30,
  name: "Mike",
  showName: f
}

*/

//  mike는 객체 내부에 showname이 있고, tom은 프로토타입 내부에 showname이 있다.
// 사용법은 동일하다.
console.log(tom.showName())
```

```js
// 생성자 함수

User.prototype.showName = function (){
    console.log(this.name);
};

```



```js
// Class 상속
// extends

class Car {
    constructor(color) {
        this.color = color;
        this.wheels = 4;
    }
    drive() {
        console.log("drive..");
    }
    stop() {
        console.log("STOP!");
    }
}

class Bmw extends Car{
    park() {
        console.log("PARK");
    }
}

const z4 = new Bmw("blue")

console.log(z4)
/*
[object Object] {
  color: "blue",
  wheels: 4
}
*/
// 프로토타입에 다른 함수들이 들어가 있음(두 번 들어갈 수 있음)
```

```js
// 메소드 오버라이딩

class Car {
    constructor(color) {
        this.color = color;
        this.wheels = 4;
    }
    drive() {
        console.log("drive..");
    }
    stop() {
        console.log("STOP!");
    }
}

class Bmw extends Car{
    park() {
        console.log("PARK");
    }
    // Bmw클래스에 Car 클래스에서 정의한 것과 같은 함수가 있을 때
    stop() {
        console.log("OFF")
    }
}

const z4 = new Bmw("blue")

console.log(z4.stop()); // OFF
// z4가 Bmw를 상속했고, Bmw가 Car를 다시 상속 할 때, 이미 값이 있으면 바뀌지 않음
```

```js
// 오버라이딩 2
// 부모의 요소를 상속받고 싶다면 super키워드를 사용한다.
class Bmw extends Car{
    park() {
        console.log("PARK");
    }
    // Bmw클래스에 Car 클래스에서 정의한 것과 같은 함수가 있을 때
    stop() {
        super.stop();
    }
}
```

```js
// 생성자 오버라이딩
class Car {
    constructor(color) {
        this.color = color;
        this.wheels = 4;
    }
    drive() {
        console.log("drive..");
    }
    stop() {
        console.log("STOP!");
    }
}

class Bmw extends Car{
    constructor(color){
        super(color);
        this.navigation = 1;
    }
    park() {
        console.log("PARK");
    }
}

const z4 = new Bmw("blue")
// Bmw의 this가 실행될 때 Car의 this를 잃어버리기 때문에
// Bmw에서 다시 super를 사용해서 Car의 요소를 받아야 한다.
```



---

#### Promise

- 기본 구조

  ```js
  const pr = new Promise((resolve, reject) => {
      //code
  });
  
  /*
  new Promise 로 생성
  인수는 resolve와 reject
  resolve는 성공한 경우, reject는 실패했을 때 실행
  resolve와 reject와 같이 
  어떤 일이 완료 된 이후 실행되는 함수를 callback 함수라 한다.   
  */
  ```

  ```js
  const pr = new Promise((resolve, reject) => {
      setTimeout(()=>{
          resolve('OK')
      }, 3000)
  });
  
  /*
  해당 코드는 
  state : pending(대기)
  result : undefined
  였다가 3초 후
  state : fulfilled(이행됨)
  result: 'OK'
  로 변한다.
  */
  ```

  ``` js
  const pr = new Promise((resolve, reject) => {
      setTimeout(() => {
          reject(new Error('error..'))
      }, 3000)
  });
  
  /*
  해당 코드는
  state : pending
  result : undefined
  였다가 3초후
  state: rejected(거부됨)
  result : error
  로 바뀜
  */
  ```

  ```js
  const pr = new Promise((resolve, reject) => {
      setTimeout(()=>{
          resolve('OK')
      }, 3000)
  });
  
  pr.then(
      // 이행 되었을 때
      function(result){
          console.log(result+'가지러 가자.'); //result 는 OK
      },
      // 거부되었을 때
      function(err){
          console.log('다시 주문해주세요..');
      },
  );
  
  // 다음과 같이 바꿀 수 있음
  // catch는 reject인 경우에만 사용 가능
  pr.then(
      function(result){}
  ).catch(
      function(err){}
  )
  
  // catch문을 사용하는 것이 가독성 부분이나 오류수정 부분에서 좋다.
  ```

  ```js
  pr.then(
      function(result){}
  ).catch(
      function(err){}
  ).finally(
      function(){
          console.log('--- 주문 끝---')
      }
  )
  ```



---

#### async, await

```js
async function getName(){
    return "Mike";
}
// async 키워드를 붙여주면, 항상 promise를 반환

console.log(getName()); //[object Promise] {...}

getName().then((name)=>{
    console.log(name);
}); //"Mike"
```

```js
function getName(name) {
    return new Promise((resolve, reject) => {
        setTimeout(()=> {
            resolve(name);
        }, 1000);
    });
}
async function showName(){
    const result = await getName('Mike');
    console.log(result);
}
// await는 async 함수 내부에서만 사용 가능
// await 오른쪽에는 pormise가 오고, pomise가 처리될 때까지 기다린다.

console.log("시작");
showName(); 
// 코드 실행하면 '시작'출력 하고 1초 후에 Mike 출력

//result에 getName에서 resolve된 값을 기다렸다가 넣어주는 것.
```



---

#### Generator

함수의 실행을 중간에 멈췄다가 재개할 수 있는 기능

다른 작업을 하다가 다시 돌아와서 next()해주면 진행이 멈췄던 부분부터 이어서 실행

```js
// 함수에 별(*)을 써서 만들고, 함수 내부에 yield 키워드를 사용
// next(), return(), throw() 매서드를 가짐
function* fn() {
    console.log(1);
    yield 1;
    console.log(2);
    yield 2;
    console.log(3);
    console.log(4);
    yield 3;
    return "finish";
}

const a = fn();

console.log(a.next()) // 1, {done: false, value: 1}
console.log(a.next()) // 2, {done: false, value: 2}
console.log(a.next()) // 3, 4, {done: false, value: 3}
console.log(a.next()) // {done: true, value: finish}
console.log(a.next()) // {done: true, value: undefined}

console.log(a.return('END')); // {done: true, value: "END"}
console.log(a.next()) // {done: true, value: undefined}

console.log(a.throw(new Error('err'))); //{done: true, value: undefined}
// catch문에 있는 error 코드가 실행됨
```

- iterable

  반복 가능하다.

  Symbol.iterator 메서드가 있다.

  Symbol.iterator는 iterator를 반환해야 한다.



- iterator

  next 메서드를 가진다.

  next메서드는 value와 done 속성을 가진 객체를 반환한다.

  작업이 끝나면 done은 true가 된다.

```js
const arr = [1, 2, 3, 4, 5];

const it = arr[Symbol.iterator()];
console.log(it.next()); //{value:1, done: false} 
```

