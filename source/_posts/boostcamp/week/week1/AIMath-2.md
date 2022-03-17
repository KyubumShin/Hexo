---
title: 부스트 캠프 ai tech 1주 3일차 Ai Math (2)
date: 2022-01-19 12:37:16
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
이 글에서 미분은 다루지 않습니다

## 3. 경사하강법
* 함수의 극소값의 위치를 구할때 사용하는 방법
* 현재값의 기울기를 이용하여 점점 극소값에 접근한다
* 기울기가 너무 커서 발산할 경우를 방지하기 위해 lr(learning rate)를 곱해서 충분히 작은 값으로 계산을 해준다
* 컴퓨터로 계산할 경우 딱 떨어지는 정수를 만들어내기 힘들기 때문에 $\epsilon$ 값보다 작아질 경우를 수렴했다라고 가정한다  

$$
x_{i+1} \leftarrow  x_{i} - \gamma \nabla f(x_{i})
$$

* python code
```python
var = init # 초기값
grad = gradient(var) # 현재 위치로부터 기울기를 구하는 함수
while (abs(grad) > eps):
    var += - lr * grad
    grad = gradient(var)
```

* 벡터가 입력인 다변수 함수의 경우는 편미분을 이용하여 경사하강법을 진행한다

### 3.1 선형회귀에서의 경사하강법
* 선형회귀에서의 target은 $\left\\|\mathbf{y-X\beta}\right\\|\_{2}$ 이고, 이를 최소화하는 $\beta$를 찾아야 하기 때문에 아래와 같은 gradient를 구해야 한다  

$$
\nabla_{\beta}\left\\|\mathbf{y-X\beta}\right\\|\_{2}=-\frac{\mathbf{X^{\top}(y-X\beta)}}{n\left\\|\mathbf{y-X\beta}\right\\|\_{2}}
$$

* 위의 식을 통하여 $\beta$를 구하는 경사하강법 알고리즘은 아래와 같다

$$
\begin{eqnarray\*}
\beta_{i+1}&\leftarrow\beta_{i}-\gamma\nabla_{\beta}\left\\|\mathbf{y-X\beta_{i}}\right\\|\_{2}\\\\
\beta\_{i+1}&\leftarrow\beta_{i} + \gamma \frac{\mathbf{X^{\top}(y-X\beta)}}{n\left\\|\mathbf{y-X\beta}\right\\|\_{2}}
\end{eqnarray\*}
$$

* 간략하게 아래와 같이 표현도 가능하다 
  * gradient를 최소화시키는것과 gradient의 제곱을 최소화 시키는것은 같은 의미

$$
\beta_{i+1} \leftarrow \beta_{i} + \frac{2\gamma}{n} \mathbf{X^{\top}(y-X\beta)}
$$

### 3.2 경사하강법의 한계
* 볼록한 함수에서는 적절한 학습률과 반복횟수를 선택했을 때 수렴이 보장되어있다
* 비선형회귀의 경우 목적식이 볼록하지 않기 때문에 수렴이 항상 보장되지는 않는다
* 특히 딥러닝의 경우 고차원의 자료를 다루기 때문에 경사하강법만으로는 학습하기가 힘들다

<center>

![non_linear](/img/nonlinear.PNG)

</center>

* 이러한 이유로 SGD, Momentom, Adam 등의 여러가지 optimize 알고리즘이 등장했다
* 이 부분에 대해서는 추후에 따로 다룰 예정이다
