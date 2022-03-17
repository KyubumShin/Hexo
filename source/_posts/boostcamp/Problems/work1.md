---
title: Week1 Homework
date: 2022-01-21 12:22:13
tags:
- week1
categories:
- [boostcamp, Problems]
widgets: null
mathjax: true
---
***
## 1. 기초과제
* 과제 내용
  * 간단한 python의 built-in function 과 문자열 처리를 위한 과제
* 결과
  * 정규식 라이브러리 `re`를 사용하여 문자열을 처리해주었다
* 회고
  * 기초과제 + 첫주라 그런지 난이도는 어렵지 않았다
  * 문제표현상 애매한 점이있었지만, 조교님과의 소통으로 해결함

## 2. 심화과제
* 여기서부터 진정한 과제

### 1. 경사하강법 구현
* 말 그대로 경사하강법의 구현
* 차근차근 수식을 코드로 바꾸면 되기때문에 어려운부분은 없었다

### 2. BPTT 구현
* 과정
  * RNN의 Backpropagation은 처음 구현하는거라 시행착오가 많았다
* numpy를 거의 사용 안하고 문제를 풀었는데 조금 연습을 할 필요가 있어보인다


### 3. 최대가능도 계산 증명 및 구현
* 가우시안 분포를 통한 최대가능도 계산

>* 로그우도함수
$$
\begin{aligned}
L(\theta|x) &= \sum_{i=1}^{n}\left( -\frac{1}{2}\log2\pi\sigma^2 +\log \exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right) \right)\\\\
&= -\frac{n}{2}\log2\pi\sigma^2 - \sum_{i=1}^{n}\frac{(x_i-\mu)^2}{2\sigma^2}\\\\
&= -\frac{n}{2}\log2\pi\sigma^2 - \frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i-\mu)^2
\end{aligned}
$$

>* 모평균의 추정량
$$ 
\begin{aligned}
\frac{\partial L(\theta|x)}{\partial \mu}&= -\frac{1}{2\sigma^2}\sum_{i=1}^{n}\frac{\partial}{\partial \mu}\left(x_i^2-2x_i\mu+\mu^2\right)\\\\
&= -\frac{1}{2\sigma^2}\sum_{i=1}^{n}(-2x_i + 2\mu)\\\\
&= \frac{X-n\mu}{\sigma^2}\\\\
\hat{\mu} &= \frac{1}{n}X\\\\
&= \frac{1}{n}\sum_{i=1}^{n}x_i
\end{aligned}
$$

>* 모분산의 추정량
$$\frac{\partial L(\theta|x)}{\partial \sigma}  = -\frac{n}{\sigma} + \frac{1}{\sigma^3}\sum_{i=1}^{n}(x_i-\mu)^2$$ 
$$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2$$


### 후기
* 우린 앞으로 편미분과 평생을 같이 살아야한다고
* 역시 스스로 힘으로 문제를 해결하면 기분이 좋다
* 다음 심화과제는 어떨지 궁금하다