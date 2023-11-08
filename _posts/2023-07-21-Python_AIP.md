---
title: Python API
date: 2023-07-21 19:06:00 +09:00
categories: [Python]
tags:
  [
    python,
    api,
    json,
  ]
---
# Python API



```python
json_data = '''       # ''' 여러줄 문자열
{
    "name": "김싸피",
    "age": 28,
    "hoobies": [
        "공부하기",
        "복습하기",    
    ]	
}

'''
```



- 파싱 : 데이터를 의미 있는 구조로 분석하고 해석하는 과정
- json.loads() : JSON 형식의 문자열을 파싱하여 python Dictionary로 변환

- 서버 : 부탁을 받으면 처리해주거나, 부탁대로 원하는 값을 돌려주는 역할

- 클라이언트 : 부탁하는 역할

(ex. 크롬(클라이언트)가 네이버(서버)에 메인화면을 요청)



```python
import requests

url = 'https://~~'  # 요청을 보내는 서버의 주소
data = requests.get(url).json()  # requests.get(url) 해당 서버에 대에터를 달라고 요청을 보내는 함수
# json() 내부의 데이터를 json형태(파이썬의 딕셔너리와 비슷)로 변환해주는 함수
print(data)
```



- API

  클라이언트들은 각자 다른 방식으로 요청을 보낼 것이다. 그런데 서버는 어떻게 요청을 이해하고 데이터를 반환할 수 있는 것일까?

  클라이언트가 원하는 기능을 수행하기 위해서 서버 측에서 미리 프로그램을 만들어 놓았기 때문이다.

  (기능 예시 : 데이터 저장, 조회, 수정, 삭제 등)

  서버 측에 특정 주소로 요청이 오면 정해진 기능을 수행하는 API를 미리 만들어 둔다.

  클라이언트는 서버가 미리 만들어 놓은 주소로 요청을 보냅니다.

  - 서버 측에서 api를 만들고 api가 알아듣는 방식으로 요청을 보내라고 한다. api의 사용 설명은 공식 문서화해서 게시한다.

- pip : 파이썬 패키지 관리 도구

- pip install requests : requests를 설치해라

- fakestoreapi.com/carts :  쇼핑몰 가짜 데이터를 제공하는 교육용 더미데이터

- 정보를 가지고 있는 서버. 무료인가?

  무료로 개방된 api : 오플 API

  사용법은 공식문서(Docs)에 명시되어 있다.

- 오픈 API 주의사항

  오픈 API는 API KEY를 활용하여 사용자를 확인한다. (내용 증명)

  사용자 인증 혹은 회원가입을 하면 서버에서 API KEY를 발급해 준다.

  서버를 요청할 때 마다 해당 API KEY를 함께 보내 정상적인 사용자인 것을 확인 받는다.

  일부 오픈 API는 사용량이 제한된다.  / 사용량이 초과될 경우 요금이 청구될 수 있다.



- JOSN(자바스크립트 객체 표기법)

  경량의 텍스트 기반의 데이터 형식

  프로그래밍 문법이 아니라 단순히 데이터를 표현하는 방법 중 하나



- 특징

  데이터는 중괄호 {}로 둘러싸인 키-값 쌍의 집합으로 표현됨 (dict와 유사)

  키 = 문자열 / 값 = 다양한 데이터 유형을 가질 수 있다.

  값은 쉽표(,)로 구분된다.

  ​	

---

### 기타 메모

- 기획을 할 때 생각할 것.

  확실한 가치, 컨셉, 최신 기술, 새로운 기술, 유용한 api를 잘 사용할 것.

- jupyter

```python
git bash 에서 jupyter notebook

y : 다시 코드 모드로 변경
m : 쉘 하나가 마크 다운 모드로 변경
a : 커서 기준 위에 쉘 하나 추가
b : 커서 기준 아래에 쉘 하나 추가
dd 쉘 삭제
shift enter : 실행 후 커서 아래로 이동
crtl enter : 실행 후 커서 제자리
```

- 예시

  ```python
  API_KEY = ''
  
  urt = f'url'
  
  import requests
  
  response = requests.get(url).json()
  response[][]  # 원하는 딕트 꺼내기
  ```

  

- vscode에서 오류나거나 한글 깨질 때

  우클릭 해서 - run python - run python file in terminal에서 실행해보기

  python (파일명).py

  파일 경로 확인.
