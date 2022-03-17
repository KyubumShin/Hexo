---
title: Functools.Partial
date: 2022-03-10 15:00:21
tags:
- week8
- Python
- Function
categories:
- Programming
- Python
- tip
widgets: null
mathjax: true
---
***
과제를 하다가 functools의 partial을 쓸 기회가 있었는데 오류를 뱉어서 나름대로 해결을 하고 정답지를 보니 작성한 코드가 달라서 한번 조사해보고 쓰는 글입니다.  

## Functools의 Partial에 대해 알아보자
* functools Module의 내장 함수인 Partial은 기존에 존재하는 함수에 추가적인 인수를 지정하여 새로운 버전의 함수로 만들어주는 기능을 가지고 있다.

## Partial의 예시
말로만 설명하면 이해하기 힘드니 코드와 같이 보자  

다음과 같이 n진수를 10진수의 형태로 바꾸어 주는 함수가 있다고 하자
```python
def to_int(num, base):
    return int(num, base=base)
```

이때 특정한 수 2와 3을 Base로 하는 함수를 원한다고 할 때 다음과 같이 사용할 수 있다.

```python
def two_to_int(num):
    return to_int(num, base=2)

def three_to_int(num):
    return to_int(num, base=3)
```

하지만 매번 특정한 수를 Base로 하는 함수를 이렇게 여러줄로 정의하면 코드의 줄도 길어지고 귀찮을수 있는데 이때 Partial을 사용하면 다음과 같이 함수를 새로 정의할 수 있다.

```python
two_to_int = partial(to_int, base=2)
three_to_int = partial(to_int, base=3)

two_to_int("10")
2
three_to_int("120")
15
```

## 내부 구조
Partial 함수는 아래 코드와 같이 정의되어있다

여기서 2가지 방법으로 함수의 인자를 미리 설정할 수 있다.
* partial(함수이름, 변수)
  * newfunc.args에 변수를 저장한다
* partial(함수이름, 변수명=변수)
  * newfunc.keywords에 변수명이 Key, 변수가 value로 저장된다
  * 기존에 있는 변수를 변수명을 통해서 다시 지정할 때 그 변수의 입력위치가 중간에 존재할 경우 Error가 발생한다

```python
def partial(func, /, *args, **keywords):
    def newfunc(*fargs, **fkeywords):
        newkeywords = {**keywords, **fkeywords}
        return func(*args, *fargs, **newkeywords)
    newfunc.func = func
    newfunc.args = args
    newfunc.keywords = keywords
    return newfunc
```

* 함수가 실행될때는 newfunc.args에 저장된 args, 함수에 입력되는 parameter, newfunc.keywords 순으로 순차적으로 입력된다  

```python
def tempfunc(one, two, three, four):
    print(one, two, three, four)

a = partial(tempfunc, 1, 2)
a(5, 3)
output
1 2 5 3

a = partial(tempfunc, two=1)
a(5, 3, 2)
output
TypeError: tempfunc() got multiple values for argument 'two'
```

### reference
* [Functools 의 Partial 이란?](https://hamait.tistory.com/823)
* [functools — Higher-order functions and operations on callable objects](https://docs.python.org/3/library/functools.html)