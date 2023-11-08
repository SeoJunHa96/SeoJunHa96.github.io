---
title: Python Data Structure 1
date: 2023-07-24 19:06:00 +09:00
categories: [Python]
tags:
  [
    python,
    data,
    method,
  ]
---

# Python Data Structure 1

#### 메서드 : 객체에 속한 함수

- 객체의 상태를 조작하거나 동작을 수행
- 문자열, 리스트, 딕셔너리 등 각 데이터 구조의 메서드를 호출하여 다양한 기능 활용
- 메서드는 클래스 내부에 정의되는 함수
- 클래스는 파이썬에서 타입을 표현하는 방법
- 매서드는 어딘가(클래스)에 속해 있는 함수이며, 각 데이터 타입별로 다양한 기능을 가진 메서드가 존재



- 호출 방법

  ```python
  'hello'.capitalize()
  # 데이터 타입 객체. 메서드()	
  
  # 예시
  numbers = [1, 2, 3]
  numbers.append(4)
  
  print(numbers)  # [1, 2, 3, 4]
  ```



- 메서드가 객체에 속한 함수라는 것은 닷(.)을 기점으로 왼쪽에 있는 객체를 어떻게 조작하거나 동작하게 만드는 함수라고 생각하면 된다. 그리고 각 데이터 타입마다 다양한 기능을 가진 메서드가 존재한다.
- 알고리즘 문제 풀이 등을 통해서 언제, 어떻게 메서드가 필요한지 공부하는 것이 중요.

---



- 시퀀스 타입(Sequence Types)

  여러 개의 값들을 순서대로 나열(정렬이 아님)하여 저장하는 자료형

  각 값에 고유한 인덱스를 가지고 있으며, 이를 사용하여 특정 위치 값을 선택하거나 수정할 수 있다.

  인덱스 범위를 조절해 부분적인 값 추출

  len() 함수를 사용하여 저장된 값의 개수를 구할 수 있다.

  저장된 값들을 반복적으로 처리할 수 있다.

  

- 문자열 조회/탐색 및 검증 메서드(str)

  ```python
  s.find(x)  # x의 첫 번째 위치를 반환. 없으면 -1을 반환
  print ('banana'.find('a'))  # 1
  
  s.index(x)  # x의 첫 번째 위치를 반환. 없으면 오류 발생
  print('banana'.index('a'))  # 1  # 없으면 ValueError가 발생
  
  ## error가 발생하면 프로그램이 중단되기 때문에 상황에 따라서 사용한다.
  
  s.isaplha()  # 알파벳 문자 여부(단순 알파벳이 아니라 유니코드 상 Letter)
  # 문자열이 알파벳만으로 이루어져 있는지 확인. T/F로 반환.
  ## 한글도 T이지만 공백, 숫자가 포함되면 F이다.
  
  s.isupper()  # 대문자 여부
  s.islower()  # 소문자 여부
  # 문자열이 모두 대문자/소문자로 이루어져있는지 확인. T/F로 반환
  
  s.istitle()  # 타이틀 형식 여부
  ```



- 문자열 조작 메서드(새 문자열 반환)

  ```python
  s.replace(old, new[,count]) # 바꿀 대상 글자를 새로운 글자로 바꿔서 반환
  text = 'Hello, world!'
  new_text = text.replace('world', 'Python')
  print(new_text)  # Hello, Python!
  
  s.strip([chars])  # 문자열의 시작과 끝에 있는 공백 혹은 특정 문자를 제거
  1) text = '     hello, world!    '
  new_text = text.strip()
  print(new_text)  # 'Hello, world!'
  2) 'www.example.com'.strip('cmowz.')  # example
  
  s.split(sep=None, maxsplit=-1)  # 공백이나 특정 문자를 기준으로 분리, 문자열의 리스트로 반환
  text = 'Hello, world!'
  words = text.split(',')
  print(words)  # ['Hello', ' world!']
  words = text.split('o')
  print(words)  # ['Hell', 'w', 'rld']  # 문자열로 하면 특정 문자는 삭제된다, 모든 특정한 문자열에 해당한다.
  
  
  'separator'.join([iterable])  # 구분자로 iterable을 합침
  iterable 요소들을 원래의 문자열을 구분하여 이용하여 하나의 문자열로 연결(split 의 반대)
  words = ['Hello', 'world!']
  text = '-'.join(words)
  print(text)  # 'Hello-world!'
  
  s.capitalize()  # 가장 첫 번째 글자 대문자로 반환(원본은 변경되지 않음.)
  s.title()  # 문자열 내 띄어쓰기 기준으로 각 단어의 첫 글자는 대문자로, 나머지는 소문자로 변환
  'Hello world'.title()  #'Hello World'
  
  s.upper()  # 모두 대문자로 변경
  s.lower()  # 모두 소문자로 변경
  s.swapcase()  # 대, 소문자 서로 변경
  ```



- 메서드는 이어서 사용 가능

  ```python
  text = 'heLLo, woRld!'
  new_text = text.swapcase().replace('l', 'z')
  print(new_text)  # HEzzO, World!
  ```



- 리스트 값 추가 및 삭제 메서드

  ```python
  L.append(x)  # 리스트 마지막에 항목 x를 추가
  
  L.extend(m)  # iterable m의 모든 항목들을 리스트 끝에 추가 (+=과 같은 기능)
  my_list = [1, 2, 3]
  my_list.extend([4, 5, 6])
  print(my_list)  # [1, 2, 3, 4, 5, 6]
  
  numbers = [1, 2, 3]
  numbers2 = [4, 5, 6]
  numbers.append(numbers2)
  print(numbers)  # [1, 2, 3, [4, 5, 6]]
  
  numbers.extend(numbers2)
  print(numbers)  # [1, 2, 3, 4, 5, 6]
  
  L.insetr(i, x)  # 리스트의 지정한 인덱스 I 위치에 x를 삽입
  my_list = [1, 2, 3]
  my_list.insert(1, 5)
  print(my_list)  # [1, 5, 2, 3]
  
  L.remove(x)  # 리스트에서 첫 번째로 일치하는 항목을 삭제
  my_list = [1, 2, 3, 2]
  my_list.remove(2)  # [1, 3, 2]
  
  L.pop()  # append와 반대
  
  L.pop(i)  # 리스트에서 지정한 인덱스의 항목을 제거하고 반환, 작성하지 않을 경우 마지막 항목을 제거.
  my_list = [1, 2, 3, 4, 5]
  item1 = my_list.pop()  # 5
  item2 = my_list.pop(0)  # 1
  print(my_list)  # [2, 3, 4]
  
  L.clear()  # 리스트의 모든 항목 삭제
  my_list = [1, 2, 3]
  my_list.clear()
  print(my_list)  # []
  ```



- 리스트 탐색 및 정렬 메서드

  ```python
  L.index(x, start, end)  # 리스트에 있는 항목 중 가장 왼쪽에 있는 항목 x의 인덱스 반환
  my_list = [1, 2, 3]
  index = my_list.index(2)
  print(index)  # 1  ## 값을 반환하는 것이 아니라 그 값의 인덱스를 반환한다.
  
  L.reverse()  # 리스트의 순서를 역순으로 변경(정렬이 아님)
  my_list = [1, 3, 2, 8, 1, 9]
  my_list.reverse()
  print(my_list)  # [9, 1, 8, 2, 3, 1]
  
  L.sort()  # 리스트를 정렬 (매개변수 이용 가능)
  my_list = [3, 2, 1]
  my_list.sort()
  print(my_list)  # [1, 2, 3]
  # 내림차순
  my_list.sort(reverse = True)
  print(my_list)  # [3, 2, 1]
  ##
  sort()에서 reverse = False가 기본인자로 작동중
  ###
  sort()는 그 자체로 오름차순만 해줄 뿐 새로운 값을 도출하지는 않는다.
  
  
  L.count(x)  # 리스트에서 항목 x의 개수를 반환
  my_list = [1, 2, 2, 3, 3, 3]
  count = my_list.count(3)
  print(count)  # 3
  ```



- 문자열에 포함된 문자들의 유형을 판별하는 메서드

  ```python
  isdecimal()  # 문자열이 모두 숫자 로만 이루어져 있는 경우 True
  ## 모든 문자가 십진수 문자이고, int형으로 변환 가능한 숫자만 True
  
  isdigit()  # isdecimal()과 비슷하지만, 유니코드 숫자도 인식('③'도 숫자로 인식)
  ## 십진수 문자, 호환성 위 첨자 숫자와 같은 특수 처리가 필요한 숫자 포함.
  ### 숫자 모양으로 생겼으면 true, 분수는 안됨.
  
  isnumeric()  # 몇 가지 추가적인 유니코드 문자들을 인식, 분수 지수 루트 기호도 숫자로 인식
  ## digit, 숫자 값 속성을 갖는 모든 문자 포함.
  ### 제곱근, 분수, 거듭제곱 특수문자 등의 특수문자도 True
  
  단 -가 들어가는 음수의 경우 '-'가 문자형으로 인식되기 때문에 문자 취급된다.
  ```

  

- sort메서드

  ```python
  sort
  print(numbers.sort())  # None 
  
  numbers = [3, 2, 1]
  print(sorted(numbers))  #[1, 2, 3] 원본을 바꾸지는 않음
  print(numbers)  #[3, 2, 1]
  ```



- ```python
  numbers = [1, 2, 3]
  
  # 1. 할당
  list1 = numbers
  
  # 2. 슬라이싱
  list2 = numbers.[:] # 전체를 자르는 것.
  
  numbers[0] = 100
  print(list1)  # [100, 2, 3]  ## 원본에 따라서 바뀜   ### 원본 numbers가 list1이 된 것
  print(list2)  # [1, 2, 3]  # 잘라서 할당한 경우에는 안바뀜 ### numbers를 슬라이싱 한 '값'이 list2가 된 것 #### 따라서 numbers가 바뀐다 하더라도 list2가 바뀌진 않음.
  
  ```



- 중요 내용

  split, join, append, extend, pop, reverse, sort 

---

#### 기타 메모



- EBNF 표현법 확인



- 객체 지향 프로그래밍
  - 객체 : 어떠한 속성값과 행동을 가지고 있는 데이터, 객관적인 실체.
  -  컴퓨터 프로그램으로 해결해야 하는 문제를 실제 세상에서 처럼 다양한 정보들을 가진 객체들로 표현하고, 그 객체들간 통신으로 해결하는 기법



- 얕은 복사

  값을 한번 복사했지만 따로 존재.

  ```python
  e = [1, 2]
  f = e[:]
  
  e[0] = 10
  print(e, f)  # [10, 2] [1, 2]
  
  # list가 하나일 때는 가능하지만 중첩 리스트일 때는 중첩 리스트 안의 요소는 같이 바뀐다.
  
  g = [1, 2, [3, 4]]
  h = g[:]
  
  g[2][0] = 30
  print(g, h)  #[1, 2, [30, 4]] [1, 2, [30, 4]]
  ```

  



- 깊은 복사

  ```python
  import copy
  
  copy.deepcopy()
  
  # 모양만 갖게 복사, 전부 따로 데이터 참조.
  ```

  

