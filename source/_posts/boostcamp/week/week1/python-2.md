---
title: 부스트 캠프 ai tech 1주 2일차 Python Basic for AI (2)
date: 2022-01-18 09:39:17
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
~~1일차 배운내용 2일차에 정리하는중...~~
***
## 4. Function(함수)
* 어떤 일을 수행하는 논리적인 코드 단위
* parameter, indentation(들여쓰기), return 등으로 구성된다
* argument : 함수를 호출할 때 입력되는 파라미터들을 말한다  

```python
def im_function(im_parameter): #함수의 정의와 파라미터
    im_return = im_parameter # 수행 내용
    return im_return # 리턴값

result = im_function(im_argument)
```
* 함수에 return 값이 존재하지 않을경우 함수는 None을 리턴한다

### 4.1 지역변수 & 전역변수
* 지역변수(local variable) : 함수 내에서만 사용되는 변수
* 전역변수(global variable) : 프로그램 전체에서 사용하는 변수
  * global을 사용하여 함수내에서 정의 할 수 있다.

```python
def function(x):
  global y
  return x + y

y = 5
print(function(6)) # 11
```


### 4.2 재귀함수(recursive Function)
* 자기자신을 호출하는 함수
* 종료조건이 존재하여 종료조건을 만족시킬때 까지 스스로를 호출한다
* python에서는 recursivelimit가 걸려있어서 따로 sys 모듈을 통해 한도를 늘려놓아야 한다.
* ~~개인적으로 별로 안이용하고 싶음~~  

### 4.3 Function type hints & Docstring
* **Function type hints**  
  python에서는 dynamic typinig 형식으로 작성하기 때문에 별도로 자료형을 적어두지 않기 때문에 처음 함수를 사용하는 사용자가 interface를 알기 어렵다는 단점이 있다. 
  이를 해결하기 위해 type hints 기능을 제공한다.  
  * parameter와 return의 type을 알려주는 type hints  

```python
def this_is_function(var_name: var_type) -> return_type:
  pass
```

* **Docstring**  
  함수에 대한 상세 스펙(필요한 parameter, return, 수행하는 일 등등)을 사전에 작성한다.  
  세개의 따옴표로 함수명 아래에 표시한다
```python
def function(x):
  """
  this is docstring
  return parameter
  x : int
  =======
  return int
  """
  return x
```

### 4.4 python 가이드 라인
* 함수는 가능하면 짧게 작성한다
* 함수이름에 역할, 의도를 명확하게 나타낼 수 있도록 한다
* 하나의 함수에는 유사한 역할을 하는 코드만 포함한다
* parameter로 받은 값 자체를 바꾸지 않는다
* 공통 코드나 복잡한 수식은 함수로 나타낸다
* PEP8 참고해보자

## 5. input & print & fommatting
* input 함수는 콘솔창에서 문자열을 입력받는 함수이다(string 형태로 받아옴)
* print 함수는 입력받은 값을 문자열으로 출력한다
* **,** 를 사용할 경우 print문이 공백을 사이에 두고 연결된다
```python
print("name :")
name = input() # input -> 규범
print("Hello", name) # Hello 규범
```
* formatting을 통해서 출력양식의 형식을 지정할 수 있다.  
<center>

|type| 설명 |
|:---:|:---:|
|%s| 문자열(string)|
|%c| 문자 1개(character)|
|%d| 정수 (int 형)|
|%f| 부동소수(float 형)|
|%o| 8진수|
|%x| 16진수|
|%%| % 문자 자체|

</center>

* %n.m(datatype) 
  * string : n개의 문자로 맞춘다(공백으로 채운다). m 자리수까지만 나타낸다(혼용 불가)
  * int : n개의 문자로 맞춘다(공백으로 채운다). m 은 사용불가
  * float : n개의 문자로 맞춘다(공백으로 채운다). 소숫점 m자리까지 나타낸다
* Python 3.6 이후의 PEP8에 근거한 formatting
```python
name = Jone
age = 20
print(f'Hello, {name}. I am {age}.') # Hello, Jone. I am 20.
```

* 예전방식
```python
print('%s %s' % ('one', 'two')) # one two
print('%d %d'.format(1, 1)) # one two
```
