---
title: Week2 Peer Session
date: 2022-01-24 16:16:44
tags:
- week2
categories:
- boostcamp
- Peer Session
widgets: null
mathjax: true
---
***
### 1. tensor가 벡터형태 일 때 Backward를 진행하면 왜 아래와 같이 표기해야하나?
```python
a = tensor([3, 2])
b = tensor([4, 1])
Q = a*2 + b**2
Q.backward(gradient = tensor([1, 1]))
```
* Pytorch에서는 scalar 값이 아닌 tensor에서는 backward의 시작점으로 보지 않기 때문에 벡터에 따로 gradient를 지정해 줘야한다.  

### 2. optimizer.zero_grad()
* Gradient를 초기화 해주는 함수를 말한다
* 만약 초기화 해주지 않는다면 tensor가 backward 연산될때마다 grad에 더해져서 제대로 학습되지 않게 될 것이다  

### 3. GIL
* Global Interpreter Lock
* {% post_link python/GIL 'Global Interpritor Lock' %}