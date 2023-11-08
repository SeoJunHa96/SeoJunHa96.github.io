---
title: 알고리즘
date: 2023-07-31 19:06:00 +09:00
categories: [Python]
tags:
  [
    python,
    알고리즘,
    배열,
    시간복잡도,
  ]
---

# 알고리즘

---

- 사전 준비

  파이참

  새로운 프로젝트에 main.py

  새로운 파일 input.in, output.out 생성

  상단 메뉴에서 run - edit configurations - redirect input from 경로 설정, logs에 아웃풋 경로 설정

---

#### APS(Algorithm Problem Solving)

- 문제를 해결하기 위한 절차
- 좋은 알고리즘이란?
  1. 정확성
  2. 작업량 : 연산이 적을수록 좋음
  3. 메모리 사용량 : 얼마나 적은 메모리를 사용하는가?
  4. 단순성
  5. 최적성 : 더 이상 개선할 여지 없이 최적화되었는가

- 시간 복잡도

  실제 걸리는 시간을 측정.

  실행되는 명령문의 개수를 계산.

- 빅-오(O) 표기법

  시간 복잡도 함수 중에서 가장 큰 영향력을 주는 n에 대한 항만을 표시

  

---

#### 배열

- 일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조.

- 1차원 배열의 선언

  별도의 선언 방법이 없으며, 변수에 처음 값을 할당할 때 생성.

  이름 : 프로그램에서 사용할 배열의 이름

- 1차원 배열의 접근

  Arr[0] = 10  # '배열 Arr의 0번 원소에 10을 저장해라'

  Arr[idx] = 20  # '배열 Arr의 idx번 원소에 20을 저장하라.'

```python
'''
9
7 4 2 0 0 6 0 7 0
'''

arr = list(map(int, input().split()))
```

- 기본적인 입력 구조 몇 가지는 숙달되게 외워두기.



- 정렬 방식 종류

  1. 버블 정렬 O(n**2)

     인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식

     첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동한다.

     ```python
     # 배열을 활용한 버블정렬을 코드로 구현(오름차순)
     
     BubbleSort(a,N) # 정렬할 배열과 배열의 크기
         for i : N-1 -> 1  # 정렬될 구간의 끝
             for j : 0 -> i-1  #비교할 원소 중 왼쪽의 원소 인덱스
                 if a[j] > a[j+1] # 왼쪽 원소가 더 크면
                     a[j] <-> a[j+1]  #오른쪽 원소와 교환
                     
     
     def BubbleSort(a, N) : 정렬한 list, N 원소의 수
         for i in range(N-1, 0, -1) : # 범위의 끝 위치
             for j in range(0, i) : 
                 if a[j] > a[j+1] :
                     a[j], a[j+1] = a[j+1], a[j]
                     
     
     ```

     ```python
     # 예시
     
     T = int(input())    # 테스트케이스 개수
     
     for tc in range(1, T+1):
         N = int(input())
         arr = list(map(int, input().split()))
     
         for i in range(N-1, 0, -1): # i 구간의 마지막 인덱스
             for j in range(i):
                 if arr[j] > arr[j+1]:
                     arr[j], arr[j+1] = arr[j+1], arr[j]
     
         print(f'#{tc}', *arr)
         
     """
     input
     1
     5
     1 4 7 8 0
     """
     ```

     

  2. 카운팅 정렬

  3. 선택 정렬

  4. 퀵 정렬

  5. 삽입 정렬

  6. 병합 정렬



---

배열과 리스트의 구분 필요

---

- input을 어떻게 받아올 것인가



```python
input 파일에 내용

main.py에서
a = input()

# input()  #1. 1줄씩 입력 받는다.
# input()  #2. 'str'문자열로 입력받는다.


# input 유형 1.
testcase # 총 테스트 케이스 개수  -> T
N  # 몇 개의 요소가 들어온다.  -> 반복문으로
. . . . .  # N 개의 요소

"""
# 예시 input
10
5
1 2 3 4 5
7
. . .

T = int(input()) # 인풋은 str로 받기 때문에 int로 변경해준다.

for tc in range(1, T+1):
    # 10번이 돌 예정
    N = int(input()) # 10번의 N을 받은 것이다.
    lst = list(map(int, input().split()))
    
    print(f'#{tc}')

"""

```

```python
T = int(input())    # 테스트케이스 개수

for tc in range(1, T+1):
    N = int(input())
    arr = list(map(int, input().split()))

    for i in range(N-1, 0, -1): # i 구간의 마지막 인덱스
        for j in range(i):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

    print(f'#{tc}', *arr)
```

