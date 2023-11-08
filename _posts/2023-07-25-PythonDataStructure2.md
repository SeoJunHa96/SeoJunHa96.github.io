---
title: Python Data Structure 2
date: 2023-07-25 19:06:00 +09:00
categories: [Python]
tags:
  [
    python,
    data,
    비시퀀스,
  ]
---

# Python Data Structure 2

### Data structure (비시퀀스 데이터 구조)



- Set(세트)

  ```python
  s.add(x)  # 세트s에 항목 x를 추가. 이미 있다면 변화 없음
  
  s.clear()  # 모든 항목 제거
  my_set = {1, 2, 3}
  my_set.clear()
  print(my_set)  # set() 빈 세트는 소괄호로 표현하는데 빈 dict{}와 혼동하지 않기 위해 ()로 표기
  
  s.remove(x)  # 항목 x 제거, 항목 x가 없을 경우 Key error
  
  s.pop()  # 임의의 요소를 제거하고 반환  ## set은 순서가 없는 비시퀀스이기 때문에.
  
  s.discard(x)  # 항목 x를 제거  ## 없는 요소에 대해서는 remove와 달리 에러 없음.(None으로 반환)
  
  s.update(iterable)  # 세트에 다른 iterable 요소를 추가

  # add는 하나의 요소만 추가하지만 update는 여러 요소 한번에 추가 가능
  ```

- 집합에 대한 연산

  ```python
  set1 - set2  # 차집합
  set1.difference(set2) # set1에는 들어있지만 set2에는 없는 항목으로 세트를 생성 후 반환
  
  set1 & set2  # 교집합
  set1.intersection(set2)  # 둘 모두 들어있는 항목으로 세트를 생성 후 반환
  
  set1 <= set2  # set1이 set2에 포함
  set1.inssubset(set2)  # set1의 항목이 모두 set2에 들어있으면 True를 반환
  
  set1 >= set2  # set2가 set1에 포함
  set1.issuperset(set2)  # set1가 set2의 항목을 모두 포함하면 True를 반환
  
  set1 | set2  # 합집합
  set1.union(set2)  # set1또는 set2에(혹은 둘 다) 들어있는 항목으로 세트를 생성 후 반환
  
  ```

  

- dictionary : 고유한 항목들의 정렬되지 않은 컬렉션

  ```python
  D.clear()  # 딕셔너리 D의 모든 키/값 쌍을 제거
  
  D.get(k)  # 키 k에 연결된 값을 반환(키가 없으면 None을 반환)
  D.get(k,v)  # 키 k에 연결된 값을 반환하거나 없으면 기본 값으로 v를 반환
  person = {'name': 'Alice', 'age':25}
  print(person.get('name')) # Alice
  print(person.get('country'))  # None
  print(person.ger('contry', 'Unknown'))  # Unknown  
  # 키 contry에 연결된 값을 반환하고 없으면 'Unknown'을 반환
  
  D.keys()  # 딕셔너리 D의 키를 모은 객체를 반환
  print(person.keys())  # dict_keys(['name', 'age'])
  
  for k in person.keys():
      print(k)
  """
  name
  age
  """    
  
  D.values()  # 딕셔너리 D의 값을 모은 객체를 반환
  print(person.values())  # dict_keys(['Alice', 25])
  
  D.items()  # 딕셔너리 D의 키/값을 쌍을 모은 객체를 반환
  print(person.items())  # dict_items([('name', Alice),('age', 25)])
  
  for k, v in person.items():
      print(k, v)
      
  """
  name Alice
  age 25
  """
    
  D.pop(k)  # 딕셔너리 D에서 키 k를 제거하고 연결됐던 값을 반환 (없으면 KeyError)
  D.pop(k, v)  # 딕셔너리 D에서 키 k를 제거하고 연결됐던 값을 반환 (없으면 v 반환)
  
  print(person.pop('age'))  # 25
  print(person)  # {'name':'Alice'}
  print(person.pop('country', None))  # None
  print(person.pop('country'))  # KeyError
  
  D.setdefault(k[, default])  # 딕셔너리 D에서 키 k와 연결된 값을 반환
  # 키가 없다면 default와 연결된 키를 딕셔너리에 추가하고 default를 반환
  print(person.setdefault('country', 'KOREA'))  #KOREA
  print(person)  #{'name': 'Alice', 'age':25, 'country':'KOREA'}
  ## 이미 있는 값에 대해서는 default가 수정되지는 않는다.
  
  D.setdefault(k, v)  # 딕셔너리 D에서 키 k와 연결된 값을 반환
  ## k가 D의 키가 아니면 값 v와 연결한 키 k를 D에 추가하고 v를 반환
  
  D.update(orther)
  # other 내 각 키에 대해 D에 있는 키면 D에 있는 그 키의 값을 other에 있는 값으로 대체.
  # other에 있는 각 키에 대해 D에 없는 키면 키/값 쌍을 D에 추가
  # 기존 키는 덮어씀(마지막 작성한 값이 반환됨)
  # 여러개 동시에도 가능
  
  person = {'name': 'Alice', 'age': 25}
  other_person = {'name': 'Jane', 'gender': 'Female'}
  
  person.update(other_person)
  print(person)  # {'name' : 'Jane', 'age': 25, 'gender': 'Female'}
  
  person.update(age = 50)
  print(person)  # {'name' : 'Jane', 'age': 50, 'gender': 'Female'}
  
  person.update(country = 'KOREA')
  print(person)  # {'name' : 'Jane', 'age': 50, 'gender': 'Female', 'country' : 'KOREA'}
  
  country = '나라'
  person.update({country : 'KOREA'})  # {'name': 'Alice', 'age': 25, '나라': 'KOREA'}
  
  
  ##
  def add_item_to_dict(input_dict, input_k, input_v):
      new_dict = input_dict.copy()
      new_dict.update({input_k: input_v})
      return new_dict
  
  my_dict = {'name': 'Alice', 'age': 25}
  result = add_item_to_dict(my_dict, 'country', 'USA')
  print(result)
  # {'name': 'Alice', 'age': 25, 'country': 'USA'}
  ```

  

### 복사

- 파이썬은 데이터에 분류에 따라 복사가 달라짐
- 변경 가능한 데이터 타입과 불가능한 데이터 타입을 다르게 다룸



- 변경 가능한 데이터 타입의 복사

  주소값을 할당하기 때문에 함께 변경된다.



- 변경 불가능한 데이터 타입의 복사

  값을 공유한 것이기 때문에 변경되지 않는다.



- 복사 유형

  - 할당, 참조에 의한 복사

    리스트 복사 예시

    ```python
    original_list = [1, 2, 3]
    copy_list = original_list
    print(original_list, copy_list)  # [1, 2, 3][1, 2, 3]
    
    copy_list[0] = 'hi'
    print(original_list, copy_list)  # ['hi', 2, 3]['hi', 2, 3]
    ```

    

  - 얕은 복사

    ```python
    # 슬라이싱
    a = [1, 2, 3]
    b = [:]
    print(a, b)  #[1, 2, 3][1, 2, 3]
    
    b[0] = 100
    print(a, b)  #[1, 2, 3][100, 2, 3]
    
    # copy
    c = a.copy()
    c[0] = 100
    print(a, c)  #[1, 2, 3][100, 2, 3]
    ```

    - 얕은 복사의 한계

    2차원 리스트와 같이 변경가능한 객체 안에 변경 가능한 객체가 있는 경우.

    a와 b의 주소는 다르지만 내부 객체의 주소는 같기 때문에 함께 변경됨

    ```python
    a = [1, 2, [1, 2]]
    b = a[:]
    print(a, b)  #[1, 2, [1. 2]] [1, 2, [1. 2]]
    
    b[2][0] = 100
    print(a, b)  #[1, 2, [100, 2]] [1, 2, [100, 2]]
    
    # copy도 마찬가지
    ```

    

  - 깊은 복사

    ```python
    import copy
    
    original_list = [1, 2, [1, 2]]
    deep_copied_list = copy.deepcopy(original_list)
    
    deep_copied_list[2][0] = 100
    
    print(original_list, deep_copied_list)  #[1, 2, [1, 2]] [1, 2, [100, 2]]
    ```

    내부에 중첩된 모든 객체까지 새로운 객체 주소를 참조하도록 함.



---

#### 기타 메모

- 해시테이블

  데이터를 효율적으로 저장하고 검색하기 위해 사용되는 자료 구조

  키 - 값 쌍을 연결하여 저장하는 방식

  키를 해시 함수를 통해 해시 값으로 변환하고, 이 해시 값을 인덱스로 사용하여 데이터를 저장/검색

  세트와 딕셔너리의 키는 해시 테이블을 이용하여 중복되지 않는 고유한 값을 저장

  세트 내의 각 요소는 해시 함수를 통해 해시 값으로 변환되고, 이 해시 값을 기반으로 해시 테이블에 저장

  딕셔너리의 키는 고유해야 하므로, 키를 해시 함수를 통해 해시 값으로 변환하여 해시 테이블에 저장

  따라서 세트와 딕셔너리의 키는 매우 빠른 탐색 속도를 제공, 중복값 허용하지 않음.



- 해시

  임의의 크기를 가진 데이터를 고정된 크기의 고유한 값으로 변환하는 것

  이렇게 생성된 고유한 값은 해당 데이터를 식별하는 데 사용될 수 있음

  일종의 '지문'과 같은 역할

  지문은 개인을 고유하게 식별하는 것처럼, 해시 값은 데이터를 고유하게 식별

  파이썬에서는 해시 함수를 사용하여 데이터를 해시 값으로 변환하며, 이 해시 값은 정수로 표현됨



- set의 pop메서드

  set에서 임의의 요소를 제거하고 반환

  실행할 때마다 다른 요소를 얻는다는 의미에서의 '무작위'가 아니라 '임의'라는 의미에서 '무작위'

  by arbitrary the docs don't mean 'random'



- 파이썬에서 함수의 동작 방식은 객체의 타입에 따라 달라짐

  정수와 문자열은 서로 다른 타입이며, 이들의 해시 값을 계산하는 방식도 다름

  정수의 경우, 정수 값 자체가 곧 해시 값이 됨

  즉, 정수는 항상 같은 해시 값을 가짐.

  반변, 문자열은 가변적인 길이를 가지고 있고, 이로 인해 문자열의 해시 값은 문자열의 내용에 따라 다름



- 해시 함수

  주어진 객체의 해시 값을 계산하는 함수

  해시 값은 객체의 고유한 식별자로 사용될 수 있으며, 해시 테이블과 같은 자료 구조에서 빠른 검색을 위해 사용됨

  해시 가능성(hashable)은 객체를 딕셔너리의 키나 세트의 요소로 사용할 수 있게 하는데, 이 자료 구조들이 내부적으로 해시 값을 사용하기 때문.



- [], .get(), .setdefault()

  ```python
  # 혈액형 인원수 세기
  # 결과 {'A':3, 'B':3, 'O':0, 'AB':3}
  
  blood_types = ['A', 'B', 'A', 'O', 'AB', 'AB', 'O', 'A', 'B', 'O', 'B', 'AB']
  
  # []
  new_dict = {}
  for blood_type in blood_types:  # boold_types를 순회하면서
      # 기존에 키가 이미 존재한다면,
      if blood_type in new_dict:
          # 기존의 키의 값을 +1 증가
          new_dict[blood_type] += 1
      # 키가 존재하지 않는다면 (처음 설정되는 키)
      else:
          new_dict[blood_type] = 1
  print(new_dict)
  
  # .get()
  new_dict = {}
  for blood_type in blood_types:  
      new_dict[blood_type] = new_dict.get(blood_type, 0) +1
  print(new_dict)
  
  # .setdefault()
  new_dict = {}
  for blood_type in blood_types:    
      new_dict.setdefault(blood_type, 0)
      new_dict[blood_type] += 1
  print(new_dict)
  ```

  



- 메모리 구조(Stack, Heap)

  code, data, stack, heap  영역

  

  code영역 : 실행한 프로그램의 코드가 저장되는 영역. cpu는 코드 영역에 저장된 명령어를 하나씩 가져가서 처리한다.

  

  data영역 : 메모리의 데이터 영역은 프로그램의 전역 변수와 정적 변수가 저장되는 영역

  프로그램의 시작과 함께 할당되며, 프로그램 종료시 소멸

  

  stack영역 : 잠깐 사용하고 삭제하는 데이터 저장(지역변수, 매개변수)

  해당 객체가 정의된 블록(스코프)을 벗어날 때 소멸

  함수의 호출하는 위치도 저장

  힙보다 빠름

  

  heap영역 : 사용자가 직접 관리할 수 있는, 그리고 해야만 하는 메모리 영역

  힙 영역은 사용자에 의해 메모리 공간이 '동적'(new/포인터)으로 할당되고 해제된다.

  스택보다 큰 메모리를 할당받기 위해 사용
