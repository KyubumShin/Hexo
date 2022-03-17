---
title: Week1 Peer Session
date: 2022-01-19 10:09:44
tags:
- week1
categories:
- boostcamp
- Peer Session
widgets: null
mathjax: true
---
***
## Peer Session 정리
* 일주일동안 피어세션에서 주고받았던 질문에 대해서 추려서 정리한 글이다

### 1. python 메모리 관리는 어떤 방식으로 이루어지나?
* 영상참조하면 좋을것 같다
  * https://www.youtube.com/watch?v=arxWaw-E8QQ

### 2. list 구조체의 메모리는 어떤방식으로 할당 될까
* python의 list는 다른 언어의 array와 다르게 list 내부에 여러가지 데이터 형식이 들어가는 것이 가능하다
  * linked list 형태로 data가 추가 될 때마다 그 형식에 맞는 메모리를 할당해서 연결하기 때문에 가능하다

### 3. python float의 할당 방식은 어떻게 이루어 질까? + int 형과의 비교
* python의 float 형은 64bit의 부동소수점으로 표현을 한다
* 기억 범위 : $4.9×10^{-324}\sim1.8×10^{308}$
* 부동소수점 표현
  * 부호, 지수비트, 가수비트로 나눠서 수를 표현하는 방식을 말한다
  * 자세한 설명은 따로 포스팅 할 예정이다

### 3.1 python에서 int형의 범위는 어떻게 될까
* python3 버전으로 넘어오면서 int형의 overflow가 사라졌다
* 그래서 int형으로 표현할 수 있는 범위는 메모리가 허용하는 한도내에서 무제한이다
* 조금더 자세하게 설명하자면 python2 버전에서는 int와 long 타입을 같이 사용하는 구조였는데 int의 범위가 넘어가면 자동으로 long 타입으로 넘어가는 형식이었다.
* python3에서는 아에 long 타입이 int와 결합해서 수의 크기에 따라 탄력적으로 가용메모리를 추가적으로 할당하는 Arbitrary presicion을 사용한다