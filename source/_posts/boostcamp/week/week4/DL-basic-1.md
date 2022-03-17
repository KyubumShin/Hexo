---
title: 부스트 캠프 ai tech 4주 1일차 DL Basic (1)
date: 2022-02-07 09:10:03
tags:
- DeepLearning
- week4
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Linear Neural Networks
* Data $(x_{i}, y_{i})^{N}_{i=1}$ 가 존재 할 때 $x$에 대해서 $\hat{y}$ 연산하는 선형연산함수
* $\hat{y}=Wx + b$
* $x$ : 데이터, $y$ : 라벨
* 경사하강법으로 y에 가까운 값을 계산하는 $W$와 $b$를 찾는다

***
## Multi Layer Perceptron(MLP)
* 위의 Neural Network가 여러층에 걸쳐서 쌓여있는 형태
* Layer 사이에 Non Linear transform을 한다
  * 선형연산을 2번연속으로 하는것은 연산을 한번 하는 것과 똑같다
  * $W_{1}W_{2}x = W_{1,2}x$
* NonLinear transform의 역활을 해주는것이 Activation Functions이다
* 최근에는 대부분 ReLU 계열의 Activation Function이 쓰인다
* {% post_link DL/Basic/activate-function '자주 쓰이는 Activation functions' %}
* Target $y$와 출력물 $\hat{y}$의 차이를 계산하는 loss function을 문제에 따라 잘 선택하여 사용하는 테크닉 또한 필요하다

***
## 그 외 내용
* 이론적으로 1개의 hidden layer로 대부분의 원하는 target값의 근사할 수 있다
  * 라고 하지만 이것은 매우 어렵다
  * 그만큼 Neural Network의 표현력이 좋다라는 뜻으로 받아드리는게 더 좋다.

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)