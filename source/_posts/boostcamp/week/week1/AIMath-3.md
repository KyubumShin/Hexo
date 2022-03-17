---
title: 부스트 캠프 ai tech 1주 3일차 Ai Math (2)
date: 2022-01-19 15:24:28
tags:
- Ai Math
- week1
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## 4. 딥러닝 기본
* 딥러닝은 `비선형모델`인 신경망을 이용한 기계학습이다

### 4.1 softmax 함수
* 모델의 출력을 확률로 해석 할 수 있게 변환해주는 함수
* 인공신경망에서 확률분포를 얻기위한 마지막 활성함수로 많이 사용한다
* 출력값은 항상 0~1사이로 정규화된다  
$$
f(x)\_{k} = \frac{e^{x_i}}{\sum\_{k=1}^{n}e^{x_{k}}}
$$

### 4.2 Activation Function (활성함수)
  * 실수범위에서 정의된 비선형 함수
  * 딥러닝을 비선형 모델로 만들어주는 결정적인 함수이다
  * 여러가지 종류가 있으며 ReLU계열이 제일 많이 사용되고 있다
  * 포스팅을 통해 따로 다룰 예정이다  
  
### 4.3 신경망
  * 선형모델과 활성함수를 합성한 함수이다
  * 우리가 흔히 부르는 MLP(Multi Layer Perceptron)는 여러 층의 합성신경망을 뜻한다  

>* $x$ : input  
>* $\sigma$ : Activation Function
>* $h$ : Layer output
>* $z$ : linear output
>* $W$ : weight matrix
>* $b$ : bias
$$
h = \sigma(z)\\\\
z = Wx + b\\\\
$$


### 4.4 Backpropagation
  * MLP의 weight들을 효율적으로 갱신하는 알고리즘
  * 합성함수의 미분법인 Chain-rule 기반으로 output Layer부터 input Layer로 미분을 계산해 나간다

>
$$
O = W_{2}h + b_{2}\\\\
h = \sigma(z)\\\\
z = W_{1}x + b_{1}\\\\
$$
