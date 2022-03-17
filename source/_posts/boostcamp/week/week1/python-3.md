---
title: 부스트 캠프 ai tech 1주 2일차 Python Basic for AI (3)
date: 2022-01-18 11:39:48
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 6. Condition (조건문)
* 조건에 따라 특정한 동작을 하게 하는 명령어
* python 에서는 if, elif, else의 예약어를 사용한다
* 조건을 나타내는 기준과 실행해야하는 명령으로 구성된다
* 조건이 참일때만 실행한다
```python
if age <= 13:
    print('초등학생')
elif age <= 16:
    print('중학생')
elif age <= 19:
    print('고등학생')
else:
    print('성인')
```

<center>

|비교연산자|설명|
|:---:|:---:|
| x < y|x가 y보다 작은지 검사|
|x > y|x가 y보다 큰지 검사|
|x == y|x와 y가 같은값인지 검사|
|x is y|x와 y의 메모리 주소가 같은지 검사|
|x != y|x와 y가 같은값인지 검사|
|x is not y|x와 y의 메모리 주소가 같은지 검사|
|x >= y|x가 y이상인지 검사|
|x <= y|x가 y이하인지 검사|

</center>

* c언어에서는 0은 False, 1은 True를 나타내지만, python에서는 성립하지 않는다
* 존재하면 참, 없으면 거짓으로 판단한다
* and, or, not 논리키워드와도 같이 사용한다
```python
if 1 # True
if 0 # True
if None # False
```

### 6.1 삼항연산자(Ternary operators)
* 참과 거짓만 존재하는 결과를 한줄에 표현 할 수 있다.
```python
a = 1
print('number' if isinstance(a, int) else 'not number')
```
> ## isinstance(var, datatype) -> boolean
> 데이터의 타입을 판단하는 함수

## 7. 반복문
* 정해진 동작을 반복적으로 수행하게 하는 명령문
* for, while 명령 키워드가 존재한다  

### 7.1 for 문
* iterable 한 object의 원소의 갯수 만큼 반복시켜주는 반복문
* `range`, `enumerate`등과 연계하여 사용이 가능하다
```python
for i in range(1, 10, 2):
    print(i) # 1, 3 ... 7 ,9
for i in range(10, 1, -1):
    print(i) # 10, 9, ... , 2, 1
for i, x in enumerate('apple'):
    print(i, x) # 0 a, 1 p, ... , 4 e
```

### 7.2 while 문
* 조건을 만족하는 동안 반복적으로 명령을 수행한다
```python
i = 0
while i < 5:
    print(i)
    i += 1
# output 0, 1, 2, 3, 4
```

### 7.3 반복문 제어
* break : 특정 조건에서 가장 가까운 반복문을 종료한다
* continue : 특정 조건에서 남은 명령을 skip 하고 다음 루프로 넘어간다
* else : 반복조건이 만족하지 않은경우 반복 종료시 1회 수행한다.
  * break로 반복문에서 탈출할 경우에는 수행하지 않음