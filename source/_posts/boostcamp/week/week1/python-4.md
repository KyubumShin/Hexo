---
title: 부스트 캠프 ai tech 1주 2일차 Python Basic for AI (4)
date: 2022-01-18 14:32:17
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 8. 문자열(string)
* **char들이 저장되어있는 `시퀸스` 자료형**
* 기본적으로 list와 같은 형태로 데이터를 처리한다
  * Indexing, Slicing, +, * 연산은 리스트와 동일하게 수행한다  

### 8.1 자주 사용하는 문자열 함수  

<center>

| 함수명 | 기능 |
|:---:|:---:|
|len(a)| 문자열의 문자 개수를 반환 |
|a.upper()|대문자로 변환|
|a.lower()|소문자로 변환|
|a.capitalize()|첫 문자를 대문자로 변환|
|a.strip(input) <br/> a.rstrip(input) <br/> a.lstrip(input)| 좌우/우/좌 input을 없앰|
|a.split(input)|input 기준으로 문자열을 나눠서 리스트로 반환|
|a.isdigit() <br/> a.islower() <br/> a.isupper() | 문자열이 숫자/소문자/대문자인지 여부 반환|
|a.startswith(input) <br/> a.endswith(input)|문자열이 input으로 시작/끝 나는 문자열 여부 반환|
|str.join(list)|list의 원소들을 str로 연결해서 하나의 문자열로 나타낸다 <br/> 단 list의 원소는 모두 문자열 type 이어야 한다|

</center>

### 8.2 다양한표현
* \\ (백슬래쉬) : 특수하게 사용하는 문자열을 표현하기위해서 사용한다
  * 백슬래쉬를 표현하기 위해서는 \\\\ 두번 사용하면 된다.
* \n : 줄바꿈을 의미하는 특수문자
* \t : TAB
* """문자열""" : 줄바꿈도 자유롭게 입력 가능한 문자열 표현 
* r"문자열" : 특수문자를 무시하고 그대로 출력함
```python
print(r'이건 줄바꿈 기호입니다 \n')
# output : 이건 줄바꿈 기호입니다 \n
```