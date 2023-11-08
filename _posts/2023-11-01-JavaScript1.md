---
title: JavaScript 1
date: 2023-11-03 19:06:00 +09:00
categories: [JavaScript]
tags:
  [
    JavaScript,
  ]
---

# JavaScript 1 (ver. 코딩앙마)

- 한 문장 끝날 때마다 세미콜론(;)

- 문자열 따옴표로 감싸기("", '', ``)

- 예약어(Reserved Words)는 변수로 사용할 수 없음

- alert()

  ```javascript
  name = "Mike";
  age = 30; /이런식으로 변수선언 하는 것은 비추/
  
  alert(name);
  /경고창으로 Mike 가 출력된다/
  ```

- console.log

  ```js
  console.log(age);
  
  /콘솔에 30이 출력된다./
  ```

  

- let

  ```javascript
  let name = "MIKE";
  let name = "google";
  //let을 사용하면 google이라고 변수를 재할당 할 때, 오류 발생해서 바꿀 수 있다.//
  // 두 번째 변수지정 때, let을 안붙이면 바뀜//
  ```

  

- const

  절대 바뀌지 않는 상수, 수정 불가.



- js에서 변수를 선언할 때는, 변하지 않는 값은 const, 변할 수 있는 값은 let으로 선언하기.

  모든 변수를 const로 선언하고, 나중에 변할 여지가 있는 변수만 let으로 선언

  

- 변수 설정
  - 문자와 숫자, $, _만 사용 가능하다.
  - 첫 글자는 숫자가 될 수 없음.
  - 예약어 사용 불가
  - 상수는 대문자로 (const MAX_SIZE = 99;)
  - 변수명은 읽기 쉽고 이해할 수 있게



- 문자열 안에 변수 사용법

  ```javascript
  const name = "Mike";
  const message = 'my name is ${name}';
  console.log(message)
  ```



- 숫자 변수

  - 사칙연산, 소숫점 표현 가능

    ```js
    const x = 1/0;
    consolo.log(x)
    /Infinity 출력/
    
        
    const name = "Mike";
    const y = name/2;
    console.log(y)
    /NaN(not a number) 출력/
    ```

    

- undefined

  값이 할당되지 않음.

  ```js
  let age;
  console.log(age)
  /undefined/	
  ```

   

- typeof

  타입

  ```js
  const name = "Mike";
  
  console.log(typeof 3);  /"number"/
  console.log(typeof name);  /"string"/
  console.log(typeof true);  /"boolean"/
  console.log(typeof "xxx");  /"string"/
  console.log(typeof null);  /"object"(객체형)/
  /널이 객체는 아니고, 초기 java의 오류지만 수정하지 않음/
  console.log(typeof undefined);  /"undefined"/
  ```



- 문자열 더하기 가능

  ```js
  const name = "Mike";
  const a = "나는 ";
  const b = " 입니다.";
  const age = 30;
  console.log(a + age + "살" b)
  //"나는 30살 입니다."
  ```

  

- 대화상자

  - alert 알려줌 - 메시지를 보여줌

    ```js
    alert()
    //알림창이 뜬다.
    ```

    

  - prompt 입력 받음 - 입력창이 제공됨

    ```js
    const name = prompt("이름을 입력하세요.");
    alert("환영합니다, " + name + "님");
    //입력받을 수 있는 창이 뜬다.
    
    const name = prompt("예약일을 입력해 주세요.", "2023-09-")
    //prompt는 두 개의 인자를 받을 수 있음. 메시지, 입력받을 디폴트 값
    ```

    

  - confirm 확인 받음 - 확인 받기 위한 용도.

    ```js
    const isAdult = confirm("당신은 성인 입니까?")
    //확인창이 뜬다. alert이랑 다르게 취소버튼도 있다.
    //확인을 누르면
    console.log(isAdult)
    //했을 때, 콘솔에 true가 뜬다.
    ```



- 단점

  스크립트 일시 정지

  스타일링 불가



- 형변환

   ```js
   const mathScore = prompt("수학점수"); //90
   const engScore = prompt("영어점수");  //80
   const result = (mathScore + engScore) /2;
   console.log(result)
   // 하면 4540이 출력된다.
   // prompt로 입력받은 값은 문자형이다.
   // 즉, mathScore + engScore = 9080이 된 것.
   // 숫자형이 아니더라도 나누기같은 것은 자동으로 변환되어서 계산됨(자동 형변환)
   ```

  - 명시적 형변환

    String, Number, Boolean (첫 글자 대문자.)

    ```js
    숫자 0, 빈 문자열, null, undefined, NaN 은 false로 변환
    문자열 '0', 공백 ' ' 등 나머지는 모두 true
    ```

  - 주의사항

    ```js
    Number(null) //0
    Number(undifined) // NaN
    ```



-  연산자

  ```js
  let num = 10;
  num--; //9
  num++; //11
  
  
  let result = num++;
  console.log(result); //10
  
  let result = ++num;
  console.log(result); //11
  ```

  

-  비교 연산자, 조건문

  기본적으로 파이썬과 같음

  === : 타입까지 비교

  

  - 조건문 if, else, else if

  ```js
  if(age>19){
      console.log('환영합니다.');
  } else if(age===19){
      console.log('시험 잘 치세요');
  } else {
      console.log('안녕히 가세요.');
  }
  
  ```

  

-  논리 연산자

  - || (OR)

    OR는 첫번째 true를 발견하는 즉시 평가를 멈춤

    ```js
    const name = "Mike";
    const age = 30;
    
    if(name === 'Tom' || age>19){
    	console.log('통과');
    }
    ```

    

  - && (AND)

    AND는 첫 번째 false를 발견하는 즉시 평가를 멈춤

    조건을 고려해 최대한 검사를 안할 수 있게 코딩

    (예를 들어. 여군인데, 시력이 좋고, 운전면허가 있는 사람)

    ```js
    if(name === "Mike" && age > 19){
        console.log('통과');
    } else {
        console.log('돌아가.');
    }
    ```

    

  - ! (NOT)

  

  - 우선순위

    AND > OR > 

    ```js
    //남자이고, 이름이 Mike이거나 성인이면 통과
    const gender = 'F';
    const name = 'Jane';
    const isAdult = true;
    
    if(gender ==='M' && name ==='Mike' || isAdult){
        console.log('통과')
    } else {
        console.log('돌아가.')
    }
    // 통과
    
    // AND가 OR보다 우선순위가 높기 때문에 gender와 name이 평가가 되고, 이후에 뒷부분을 평가한다.
    // 그런데 성인이면 다 통과하기 때문에 결과가 통과가 된다.
    // flase || isAdult 가 되는 것.
    
    // 의도대로 만들려면
    if(gender ==='M' && (name ==='Mike' || isAdult)){
        console.log('통과')
    }
    ```

  

-  반복문 loop

  - for

    ```js
    for(let i = 0; i<10; i++){
        console.log(i)
    }
    
    // let i = 0; (초기값이며, 코드 실행시 1번만 작동)
    // i < 10; (조건, 반복문이 돌면서 조건을 확인하고, false가 되면 멈춘다.)
    // i++ (반복문 한번 실행 후 진행할 작업)
    ```

    

  - while

    ```js
    let i = 0;
    
    while(i<10){		// 조건
        console.log(i); // 코드 실행
        i++;			// 코드가 종료될 수 있게
    }
    ```

    

  - do.. while

    ```js
    let i = 0;
    
    do{
       console.log(i);
        i++;
    } while (i<10)
    
    // 코드 실행 후 조건 확인
    // 코드를 적어도 한 번은 실행한다는 것이 while과의 차이
    ```

    

  - break : 멈추고 빠져나옴

    ```js
    while(true){
        let answer = confirm('계속할까요?');
        if(!answer){
            break;
        }
    }
    ```

    

  - continue : 멈추고 다음 반복으로 진행

    ```js
    // 짝수만 출력
    for(let i = 0; i < 10; i++){ 
        if(i%2){  // 나머지가 0이면 false이므로 console.log를 만남
            	// 나머지가 1이면 true이므로 continue를 만남
            continue;
        }
        console.log(i)
    }
    // 결과 0, 2, 4, 6, 8 만 콘솔에 찍힌다.
    ```

    

-  switch

  모든 switch문은 if로 작성 가능하지만, 케이스가 다양할 경우 간결하게 쓸 수 있다.

  ```js
  switch(평가){
      case A:
      // A일때 코드
      case B:
      // B일때 코드
  }
  ```

  ```javascript
  let fruit = prompt('무슨 과일을 사고 싶나요?');
  
  switch(fruit){
  	case '사과':
          console.log('~원 입니다.');
         	break
      case '바나나':
  		console.log('~원 입니다.');
          break
  	case '키위':
          console.log('~원 입니다.');
          break
  	case '배':
      case '수박':
          console.log('~원 입니다.');
          break
      default : //if문의 else와 같은 역할
          console.log('그런 과일은 없습니다.')
  } 
  ```

  

-  함수(function)

  ```js
  // 기본형태
  function sayHello(name){
      console.log('Hello, ${name}');
  }
  
  /*
  함수 함수명 (매개변수){
  	함수 실행 코드
  */
  ```

  ```js
  function sayHello(name){
      let msg = 'Hello';
      if(name){
          msg += `, ${name}`;
          // += ', '+ name;
      }
      console.log(msg); 
  }
  
  ```

  ```js
  function sayHello(name){
      let newName = name || 'friend';
      let msg = `Hello, ${newName}`
      console.log(msg)    
  }
  
  sayHello(); //"Hello, friend"
  sayHello('Jane'); // "Hello, Jane"
  ```

  ```js
  function add(num1, num2){
  	return num1 + num2;
  }
  ```

  

  - tip

    함수는 한번에 한 작업만 하는게 좋다.

    읽기 쉽고 어떤 동작인지 알 수 있게 네이밍

  

-  함수 선언문

  어디서든 호출 가능

  자바 스크립트는 모든 선언된 함수를 생성해둔다.(호이스팅)

  

-  함수 표현식

  코드에 도달하면 생성

  ```js
  let sayHello = function(){
      console.log('Hello');
  } // 여기서 함수가 생성되며 사용가능해진다.
  sayHello();
  ```

  

-  화살표 함수

  ```js
  let add = function(num1, num2){
      return num1 + num2;
  }
  // 이걸 화살표 함수로 바꾸면
  let sayHello = name => `Hello, ${name}`;
  
  let add = funtion(num1, num2){
      const result = num1 + num2;
      return result;
  }
  
  ```

  

-  Object (객체)

  ```js
  // 객체 생성
  const superman = {
  	name:'clark',
      age : 33,
  }
  // 접근
  superman.name // 'clark'
  superman['age'] //33
  
  //추가
  superman.gender= 'male';
  superman['hairColor']='black';
  
  //삭제
  delete superman.hairColor;
  ```

  

-  Object - 단축 프로퍼티

  ```js
  const name = 'clark';
  const age = 33;
  
  const superman = {
  	name, //name:name
  	age, //age:age
  	gender: 'male',
  }
  ```

  

-  for - in 반복문

  ```js
  for(let key in superman){
      console.log(key)
      console.log(superman[key])
  }
  ```

   

  ```js
  // 객체 생성
  const superman = {
      name : 'clark',
      age : 30
  }
  
  // 객체를 반환하는 함수
  function makeObject(name, age){
      return{
          name : name,
          age : age,
          hobby : 'football'
      }
  }
  
  const Mike = makeObhect('Mike', 30);
  console.log(Mike) // 오브젝트 안에 마이크의 정보가 출력됨
  
  //프로퍼티 존재 확인
  console.log('age' in Mike) // 마이크 안에 age가 있는지 확인
  //없다면 false 가 출력
  
  //나이확인
  function isAdult(user){
      if(!('age' in user) || //user에 age가 없거나
         user.age < 20){     // 20살 미만이거나
          return false;
      }
      return true;
  }
  
  const Mike = {
      name : 'Mike',
      age : 30
  }
  
  const Jane = {
      name : "Jane"
  }
  
  console.log(isAdult(Mike)) // true
  console.log(isAdult(jane)) // false, 나이가 없으면 성인이 아니라고 판단
  ```

  ```js
  const Mike = {
      name : 'Mike',
      age : 30
  }
  for(x in Mike){
      console.log(x)
  }
  // "name"
  // "age"
  
  for(x in Mike){
      console.log(Mike[x]) //
  }
  // "Mike"
  // 30 
  // for 문이 Mike안에 정의되어 있는 요소 수 만큼 반복.
  ```

  

-  객체 method / this

   ```js
   const superman = {
   	name : 'clark',
       age:33,
       fly : function(){
           console.log('날아갑니다.')
       }
   }
   
   superman.fly(); // 날아갑니다.
   
   // funtion 생략가능
   
   ...
   	age:33,
       fly(){
           console.log('날아갑니다.')
       }
   }
   ```

   ```js
   const user = {
       name:'Mike',
       sayHello : funtion(){
       	console.log(`Hello, I'm${this.name}`);
   	}
   }
   ```

   - 화살표 함수는 일반 함수와는 달리 자신만의 this를 가지지 않음.
   - 화살표 함수 내부에서 this를 사용하면, 그 this는 외부에서 값을 가져 옴

   ```js
   let boy = {
       name: "Mike",
       showName : funtion(){
       console.log(this.name)
   	}
   };
   
   let man = boy;
   boy = null;
   man.showName(); //'Mike'
   ```

   - this에 대해서 좀 더 공부 필요!!

     

   - 화살표 함수 : 객체 메소드에서 화살표 함수는 윈도우를 가르킨다.

   ```js
   let boy = {
       name:"Mike",
       sayThis:() =>{
           console.log(this);
       }
   };
   boy.sayThis(); //에러, window
   ```

   

-  배열 Array

   ```js
   let students = ['철수', '영희',... '영수'];
   
   console.log(students[0]); //철수
   
   //수정
   students[0] = '민정';
   ```

   - 특징

     문자 뿐 아니라, 숫자, 객체, 함수' 등도 포함할 수 있음.

   ```js
   // length : 배열의 길이
   students.length //30
   
   //push() : 배열의 끝에 추가
   let days = ['월', '화', '수'];
   days.push('목')
   console.log(days) //['월', '화', '수', '목']
   
   // pop(): 배열 끝 요소 제거
   
   //shift, unshift : 배열 앞에 제거/추가
   days.unshift('금', '토', '일');
   console.log(days) //['금', '토', '일', '월', '화', '수']
   
   // 반복문  for
   let days = ['월', '화', '수'];
   for(let index = 0; index < days.length; index++){
       console.log(days[index])
   }
   ```

   

-  반복문 for

   ```js
   let days = ['월', '화', '수'];
   
   for(let index = 0; index<days.length; index++){
       console.log(days[index])
   }
   
   // 이게 더 좋다.
   for(let day of days){
     console.log(day)
   }
   ```

   

   





- js 알고리즘 관련 정보

  https://velog.io/@nahyunbak/JS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Math-%EA%B0%9D%EC%B2%B4
