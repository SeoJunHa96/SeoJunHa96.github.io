---
title: Data Types
date: 2023-11-03 19:06:00 +09:00
categories: [Python]
tags:
  [
    python,
    data types,
    collection,
  ]
---

# Data Types

---

#### 중요 내용

| 컬렉션 | 변경 가능 여부 | 나열, 순서 |          |
| :----: | :------------: | :--------: | :------: |
|  str   |       X        |     O      |  시퀀스  |
|  list  |       O        |     O      |          |
| tuple  |       X        |     O      |          |
|  set   |       O        |     X      | 비시퀀스 |
|  dict  |     O(key)     |     X      |          |

- 컬렉션

  변수는 하나의 값만 가진다. But. 여러 개를 담고 싶다는 니즈를 충족시키기 위해.

- Sequence(시퀀스)

  순서가 있다.

- 인덱스 : 시퀀스 내의 값들에 대한 고유한 번호, 각 값의 위치를 식별하는 데 사용되는 숫자(ex. 책갈피)

  순서가 있기 때문에 몇 번으로 갈 것인지 정할 수 있음

- 슬라이싱

  순서가 있기 때문에 나열시켜서 몇 번에서 몇 번까지 자르는 행위

- step

  |       |  h   |  e   |  l   |  l   |  o   |
  | :---: | :--: | :--: | :--: | :--: | :--: |
  | index |  0   |  1   |  2   |  3   |  4   |
  | index |  -5  |  -4  |  -3  |  -2  |  -1  |

  my_str[0:5:2] = hlo # 0부터 5까지 2칸씩 띄어서 

  my_str[::-1] : 역순

  *(#글자 수를 셀 때, 글자 자체보다 글자가 담긴 칸 앞부분을 센다고 생각하자.)*



- list : 여러 개를 담기 위한 "자료 구조"이기 때문에 유연성이 높다.



- 배열 : 순서대로 되어 있어서, 안정성과 예상성이 높다.





---

### 000

- 진수 표현

​		2진수 : 0b	/	8진수 : 0o	/	16진수 : 0x

```python
print(0b10) # 2 ##2진수 binary
print(0o30) #24 ##8진수 octal
print(0x10) #16 ##16진수 hexadecimal

# 진법 변경
print(bin(12)) #0b1100
print(oct(12)) #0o14
print(hex(24)) #ox18
```

- 유한 정밀도

  한 숫자에 대해 저장하는 용량이 제한 됨

  0.666666666... 과 1.66666667은 제한된 양의 메모리에 저장할 수 있는 2/3과 5/3에 가장 가까운 값

- Floating point rounding error

  컴퓨터는 2진수를 사용, 사람은 10진법을 사용하기 때문에 사람이 사용하느 10진법의 근사값만 표시한다. 때문에 예상치 못한 결과가 나타나기도 한다.

- 실수 연산 시 해결책

  ```python
  a= 3.2 - 3.1 #0.100000000000009
  b= 1.2 - 1.1 #0.099999999999987
  
  # 임의의 작은 수 활용
  print(abs(a-b)) <= 1e=10) # True
  
  # math 모듈 활용
  import math
  print(math.isclose(a,b)) #True
  ```

- 지수 표현 방식

  e : 10^

  ```python
  #314 * 0.01
  number = 314e-2 #314의 10의 -2제곱 = 3.14
  
  #float
  print(type(number))
  
  #3.14
  print(number)
  ```

- Sequence Types

  여러 개의 값들을 순서대로 나열하여 저장하는 자료형

  ```python
  특징
  1. 순서 : 값들이 순서대로 저장(정렬X)
  2. 인덱싱 : 각 값에 고유한 인덱스(번호)를 가지고 있으며, 인덱스를 사용하여 특정 위치의 값을 선택하거나 수정할 수 있다.
  3. 슬라이싱 : 인덱스 범위를 조절해 부분적인 값을 추출할 수 있음
  4. 길이 : len함수를 사용하여 저장된 값의 개수(길이) 구할 수 있다.
  5. 반복 : 반복문을 사용하여 저장된 값들을 반복적으로 처리 가능
  ```

  

  1. str(문자열) : 문자들의 순서가 있는 변경 불가능한 시퀀스 자료형

     작은 따옴표 또는 큰 따옴표로 감싸서 표현

     실로 묶여 있다는 의미

     변경 불가 이유  : 문자들의 나열을 보장, 문자들의 의미

     ```python
     print('Hello, World')
     print(type('Hello, World!')) #str
     ```

     - Escape sequence

     역슬래시 '\\\'뒤에 특정 문자가 와서 특수한 기능을 하는 문자 조합

  ``` python
  #파이썬의 일반적인 문법 규칙을 잠시 탈출한다는 의미
  \n 줄바꿈
  \t 탭
  \\ 백슬래시
  \' 작은 따옴표
  \" 큰 따옴표
  ```

  - - string interpolation

      문자열 내에 변수나 표현식을 삽입하는 방법

  ```
  #f-string 응용
  greeting = 'hi'
  print(f'{greeting:^10}') 가운데 정렬
  print(f'{greeting:>10}') 우측 정렬
  f-string 어드바이스?
  
  ptint(f'{3.141592:.4f}') : 소숫점 4자리까지 출력
  
  
  ```

  - - 슬라이싱

    ```python
    my_str[2:4] #문자 앞의 공백으로 생각해서 자르기.
    			#2>=, 4<
    my_str[:3] # <3
    my_str[3:] # 3>=
    
    #step
    my_str = hello
    my_str[0:5:2] # hlo ##0에서 5까지 2칸씩 뛰면서
    
    #음수 인덱스
    -는 왼쪽으로
    my_str[::-1] #문자열 뒤집기
    ```

    

  

  2. list : 변경 가능한 시퀀스

     - 0개 이상의 객체 포함

     - 대괄호로 표기 []

     - 데이터는 어떤 자료형도 저장할 수 있음(리스트 안에 리스트도 가능)

       ```python
       my_list = [1, 2, 3, 'python', ['hello', 'world', '!!!']]
       
       print(my_list)  # 5
       print(my_list[4][-1])  # !!!
       print(my_list[-1][1][0])  # w
       ```

     -  변경 가능

  

  3. tuple : 변경 불가능한 시퀀스 자료형

     - 0개 이상의 객체 포함

     - 소괄호 표기 ()

     - 데이터는 어떤 자료형도 저장할 수 있다.

       ```python
       my_tuple_1 = ()
       my_tuple_2 = (1,) # ','가 없다면 그냥 정수 1이 된다.
       				  # 튜플의 객체가 1개라면 ,를 붙여줘야 한다.
       my_tuple_3 = (1, 'a', 3, 'b', 5)
       ```

     - 개발자가 직접 사용하기 보다는 '파이썬 내부 동작'에서 주로 사용됨

     - 불변 특성을 사용한 안전하게 여러 개의 값을 전달, 그룹화, 다중 할당

       ```
       x, y = (10, 20)
       
       print(x)  # 10
       print(y)  # 20
       
       #파이썬은 쉼표로 튜플 생성자로 사용하니 괄호 생략 가능
       x, y = 10, 20
       ```

       

  4. range : 연속된 정수 시퀀스, 변경 불가능

     - range(n) : 0부터 n-1까지의 숫자의 시퀀스

     - range(n, m) : n부터 m-1까지의 숫자 시퀀스

     - 리스트 형 변환 시 데이터 확인 가능

       ```python
       my_range_2 = range(1, 10)
       print(list(my_range_2))  #[1, 2, 3, 4, 5, 6, 7, 8, 9]
       ```

       

- Non-sequence types

  1. dict : key - value 쌍으로 이루어진 순서와 중복이 없는 변경 가능한 자료형

     - 중괄호로 표기 {}

     - key는 변경 불가능한 자료형만 사용 가능(str, int, float, tuple, range)

     - value는 모든 자료형 사용 가능

       ```python
       my_dict_1 = {}
       my_dict_2 = {'key': 'value'}
       my_dict_3 = {'apple': 12, 'list : [1, 2, 3]'}  #2개의 요소를 가진 딕트
       ```

     - key를 통해 value에 접근

       ```python
       print(my_dict['apple'])  #12
       print(my_dict['list'])  #[1, 2, 3]
       
       #값 변경
       my_dict['apple'] = 100
       print(my_dict) #{'apple': 100, 'list : [1, 2, 3]'}
       ```

       

  2. set : 순서와 중복 없는, 변경 가능한 자료형

     - 중괄호 표기 {}

     - 수학에서의 집합과 동일한 연산 처리 가능

       ```python
       my_set_1 = set()  # 빈 세트는 ()로 표시 ## 딕셔너리와 구분 위해
       my_set_2 = {1, 2, 3}
       my_set_3 = {1, 1, 1}
       
       print(my_set_1)  # set()
       print(my_set_2)  # {1, 2, 3}
       print(my_set_3)  # {1}  ## 중복 없음
       ```

     - 세트의 집합 연산

       ```
       my_set_1 = {1, 2, 3}
       my_set_2 = {3, 6, 9}
       
       # 합집합
       print(my_set_1 | my_set_2)  # {1, 2, 3, 6, 9}
       # (| : shift + \)
       
       # 차집합
       print(my_set_1 - my_set_2)  # {1, 2}
       
       # 교집합
       print(my_set_1 & my_set_2)  # {3}
       
       
       ```

- None : '값이 없음'을 표현하는 자료형

- Boolean : 참과 거짓을 표현 (제어문, 조건, 반복문에서 주로 사용), 비교/논리 연산의 평가 결과로 사용됨

```python
# 가변 데이터의 주의사항.

list_1 = [1, 2, 3]
list_2 = list_1

list_1[0] = 100
print(list_2)  # [100, 2, 3]
```



---

실습 / 과제



- 줄바꿈

```python
print("안녕하세요\n반갑습니다\n안녕히가세요")
```

- 공백

```python
print("안녕하세요\n\t반갑습니다")
```

- f-string

```python
where = 'ssafy'
what = 'python'

print(f'저는{where}에서 {what}을 배웁니다.')
```

문자열 맨 앞에 f를 붙여주고, 중괄호 안에 변수 이름을 입력

f'문자열{변수}문자열'

- List Index

  1. 리스트명 = [요소1, 요소2, 요소3, ....]

  2. a = list() : 빈 리스트

  3. 0부터 시작한다.

     ```python
     a = [1, 2, 3]
     a[0]
     1
     a[0] + a[1]
     3
     ```

  4. 리스트 요소로 리스트가 들어갈 수 있다.

  5. 연산이 가능하다

     ```
     a = [1, 2, 3]
     b = [4, 5, 6]
     a + b
     [1, 2, 3, 4, 5, 6]
     
     a = [1, 2, 3]
     a * 3
     [1, 2, 3, 1, 2, 3, 1, 2, 3]
     
     ```

  6. 길이 구하기(리스트 요소 개수) : len(리스트명)

  7. 수정 : a[2] = 4 > a = [1, 2, 4]

  8. 삭제 : del a[1] > a = [1, 3]

  9. ```
     a[2:] : 2번째 부터
     a[:2] : 2번째 앞까지
     
     a = "hello"
     print(a[:2])
     he
     ```

  10. 추가 : append

      a.append()

  11. 정렬 : sort

  12. 뒤집기 : reverse

  13. 인덱스 반환 : 리스트에서의 위칫값

      ```python
      a.index(3)
      2
      ```

  14. 삽입 : insert

      ```python
      a.insert(0,4) #0번째 앞에 4 삽입
      a
      [4,1,2,3]
      ```

  15. 삭제 : remove

  16. 꺼내기 : pop

      pop(x) : x번째 요소를 리턴하고 그 요소 삭제

  17. 요소의 개수 세기 : count

      count(x) : x가 리스트 안에 몇 개 들어있는지

  18. 확장 : extend

      extend() 안에는 리스트만 올 수 있으며 원래의 리스트에 ()안의 리스트를 더한다.
  
- ```python
  for X, Y in information.items()
  # information의 요소에 있는 x, y 에 대해
  
      print(f'{X}: {Y}')
  # information에서 정의되어있는 X, Y값 반환
  ```

- 중복값 제거

  ```
  list(set())
  ```

- 깊은 복사

  ```python
  리스트를 복사한 후 다른 리스트를 변경해도 복사한 리스트가 변경하지 않게 하기
  
  import copy
  
  list2 = copy.deepcopy(list1)
  
  # 이후 list1의 요소를 바꿔도 list2는 복사 당시에서 바뀌지 않는다.
  
  
  ```
