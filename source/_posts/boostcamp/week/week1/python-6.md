---
title: 부스트 캠프 ai tech 1주 2일차 Python Basic for AI (6)
date: 2022-01-18 18:40:28
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 10. Pythonic Code
* Python 스타일의 효율적인 코딩기법
* `사용하면 코드를 간결하고 이쁘게 작성할 수 있다. 그리고 잘하는 사람처럼 보인다`
  * 그러니 모두 잘 익히고 사용하자  

### 10.1 **`List comprehension`**
* 기존의 list를 사용하여 간단한 list를 만드는 기법
* for 문 + list.append 보다 속도가 빠르다
* 조건문과 함께 더 다양한 list를 표현 가능하다
```python
# 기존 방법
a = []
for i in range(10):
    a.append(i)
# list comprehension
a = [i for i in range(10)] 
```

### 10.2 **enumerate & zip**
* `enumerate` 
  * for 문에서 iterable object의 element를 추출할 때 인덱스 번호와 함께 추출
```python
for i, x in enumerate('apple'):
    print(i, x) # 0 a, 1 p, ... , 4 e

list(enumerate('apple'))
output = [(0, 'a'), (1, 'p'), (2, 'p'), (3, 'l'), (4, 'e')]
```
* `zip`
  * 여러개의 list값을 병렬적으로 추출해서 하나의 list로 재결합 시킨다.
```python
a = (1, 2, 3)
b = (4, 5, 6)
print(list(zip(a, b)))
######################
[(1, 4), (2, 5), (3, 6)]
```

### 10.3 map & lambda & reduce
* `map`
  * iterable object의 element에 각각 특정한 함수를 적용할 수 있는 함수
  * 아래의 lambda와 병행하여 자주, 많이 쓰인다
  * 실행시점의 값을 생성해서 메모리를 효율적으로 사용한다
```python
def function(x):
    return x**2

a = [1, 2, 3, 4, 5]
print(list(map(function, a)))
#############################
output => [1, 4, 9, 16, 25]
```
* `lambda`
  * 함수를 따로 정의할 필요 없이 사용할 수 있는 익명 함수
  * PEP8에서 권장하지는 않지만 아직도 많이쓰고 스스로도 많이 쓰고있다
    * 어려운 문법, 테스트하기 힘듬, docstring 지원안함, 코드해석이 어려움 등등의 문제가 있다
  * 간단한 명령문인 경우 따로 정의하지 않고 lambda를 사용하는 편이다
```python
a = [1, 2, 3, 4, 5]
print(list(map(lambda x: x**2, a)))
#############################
output => [1, 4, 9, 16, 25]
```
* reduce
  * map과 비슷한 동작으로 list에 똑같은 함수를 적용해서 합쳐나간다
  * ~~2년 넘게 공부하면서 한번도 쓴적이 없다~~
  * python3 버전에서 lambda와 같이 사용을 권장하지 않는다
```python
from functools import reduce
print(reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]))
```
<center>

![reduce 이미지](/img/reduce.png)

</center>

### 10.4 `iterable object`
* 시퀸스형 자료형에서 데이터를 순서대로 추출하는 object
* object 내부적으로 __iter__와 __next__라는 함수(메서드)가 존재한다
* .iter() 와 .next() 함수로 iterable 객체를 iterator object로 사용이 가능하다
* 아래의 generator와 같이 사용하면 정말 강력한 성능을 보이게 된다
```python
cities = ["Seoul", "Busan", "Jeju"] 
iter_obj = iter(cities) 
print(next(iter_obj))
print(next(iter_obj)) 
print(next(iter_obj)) 
next(iter_obj)
==============
output:
Seoul
Busan
Jeju
Error 발생 더이상 출력할 수 있는 원소가 없음
```

### 10.5 `generator`
* iterable object를 특수한 형태로 사용해주는 함수
* object 내부의 element가 호출되는 시점에 값을 메모리에 반환한다
  * yield를 사용해서 한번에 하나의 element만 반환함
    * 이 것이 궁금하다면 python 코루틴 관련해서 찾아보는것이 좋다
* 일반적인 iterator 보다 generator가 훨씬더 적은 메모리를 사용한다
* 먼 훗날에 나올 Dataset이 generator를 이용한 object이다
```python
def my_gen():
    n = 1
    print('This is printed first')
    # Generator function contains yield statements
    yield n

    n += 1
    print('This is printed second')
    yield n

    n += 1
    print('This is printed at last')
    yield n


# Using for loop
for item in my_gen():
    print(item)

=====================
output:
This is printed first
1
This is printed second
2
This is printed at last
3
```
[예제출처](https://www.programiz.com/python-programming/generator)

* generator도 list comprehension과 유사한 형태로 표현이 가능하다
* [] 대신 ()로 표현한다.
```python
gen_ex = (n*n for n in range(500)) 
print(next(gen_ex)) # 0 1 4 ....
```  

### 10.6 function passing arguments
* 함수에 입력되는 Argument는 아래와 같이 다양한 형태를 가진다
  * Keyword arguments
    * 함수에 입력되는 parameter의 변수명을 같이 입력하여 순서에 상관없이 parameter를 지정 해 줄 수 있다
```python
def function(a, b):
    return a*2 + b

print(function(3, 5))
print(function(b=5, a=3))
=========================
output:
11
11
```

  * Default arguments
    * parameter의 기본값을 사용한다
    * 따로 argument가 입력되지 않을 경우 기본값으로 출력한다
```python
def function(a, b=0):
    return a*2 + b

print(function(3, 1))
print(function(3))

==================
output:
7
6
```  

  * Variable-length arguments(가변인자)
    * 개수가 특정되지 않은 변수를 함수의 parameter로 사용하는 방법
    * Asterist * 기호를 사용하여 argument를 나타낸다
    * 입력된 값은 Tuple로 사용할 수 있다
    * 함수에서 단 하나 존재하고, 뒤에 일반적인 argument가 존재할 수 없다

```python
def asterisk_test(a, b, *args):
    print(args)
    return a+b+sum(args)
print(asterisk_test(1, 2, 3, 4, 5))

===================================
output:
(3, 4, 5) 튜플의 형태로 존재한다
15
```

  * Keyword Variable-length arguments(키워드 가변인자)
    * Parameter의 이름을 따로 지정하지않고 입력하는 방법
    * Asterisk 두개 (**) 를 사용하여 함수의 parameter를 표시한다
    * 입력된 값은 dict type으로 사용할수 있다
    * 함수에서 단 하나 존재하고 뒤에 다른 argument가 존재할 수 없다

```python
def asterisk_test(a, b, **kargs):
    print(kargs)
    return a+b+sum(kargs.values())
print(asterisk_test(1, 2, three=3, four=4, five=5))
===================================================
output:
{'three': 3, 'four': 4, 'five': 5}
15
```

### 10.7 Asterisk
* Asterisk는 위의 가변인자와 곱하기 연산자 이외의 기능이 존재한다
* list, tuple 등의 자료형 변수 앞에 *를 붙여서 unpacking 할 수 있다
* dict type의 경우 **를 붙여서 키워드 가변인자처럼 출력이 가능하다
```python
a = [1, 2, 3, 4]
print(a)
print(*a)
b = {'one':1, 'two':2, 'three':3}
print(*b)
print(asterisk_test(1, 2, **b))
===============================
output:
[1, 2, 3, 4]
1 2 3 4
one two three
{'one': 1, 'two': 2, 'three': 3}
9
```