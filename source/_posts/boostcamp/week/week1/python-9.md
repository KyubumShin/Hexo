---
title: 부스트 캠프 ai tech 1주 3일차 Python Basic for AI (9)
date: 2022-01-19 11:34:10
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 14. Exception Handing
* 사전에 인지했거나 예측 하지못한 각종의 예외들을 대처하기위한 방법
* 개발자가 반드시 명시적으로 정의해야한다
* try ~ except  

```python
try:
    예외 발생 가능 코드
except (exception 종류):
    예외 발생시 대응하는 코드
```

* try ~ except ~ else
  * else : 예외가 발생하지 않을때 진행하는 부분  

```python
try:
    예외 발생 가능 코드
except (exception 종류):
    예외 발생시 대응하는 코드
else:
    예외가 발생하지 않을 때 동작하는 코드
```

* try ~ except ~ finally
  * finally : 예외가 발생해도 진행하는 부분  

```python
try:
    예외 발생 가능 코드
except (exception 종류):
    예외 발생시 대응하는 코드
finally:
    예외에 상관없이 동작하는 코드
```

* 기본적으로 제공하는 exception 종류 : [링크](https://docs.python.org/3/library/exceptions.html)
* raise 함수를 사용하여 강제로 Error나 Exception을 발생시킬 수 있다.

## 15. File Handing
* 코드로 파일을 처리하기 위한 방법
* 파일 처리를 위해서 open 을 사용한다
```python
f = open('파일이름', '접근모드')
...
...
f.close()
```
|모드| 설명 |
|:-:|:-:|
|r|읽기모드 - 파일 내용을 읽어올 때 사용|
|w|쓰기모드 - 파일 내용을 수정할 때 사용|
|a|추가모드 - 파일에 내용을 추가할 때 사용|
|b|바이너리 모드 - 바이너리형식으로 파일을 읽기/수정/추가할 때 사용|
|+|파일을 읽고 쓰기용으로 열기 <br/> (앞의 모드에 따라서 파일 포인터의 위치차이가 존재한다)|
|x|쓰기모드로 생성하는데 이미 파일이 존재할 경우 예외를 발생시킨다|

## 16. Logging Handling
* Log  
  프로그램이 실행되는 동안 일어 나는 정보를 말한다. 이런 기록들을 모아 분석하여 의미있는 결과를 도출 할 수 있기 때문에 Log를 따로 관리하는 모듈을 사용한다
* Python의 기본 Log 관리모듈 logging이 존재한다
* logging level에 관련한 표 : 아래로 내려갈수록 높은 레벨의 log이다  

<center>

![logging level](/img/logging.PNG)

</center>