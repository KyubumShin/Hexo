---
title: 부스트 캠프 ai tech 4주 3일차 DL Basic (6)
date: 2022-02-08 13:11:46
tags:
- DeepLearning
- week4
- Sequencial Model
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Sequential Model
### Naive sequeance model
* 과거 모든시점의 데이터를 고려해야한다
* 시퀸스가 진행될 수록 고려해야할 데이터 양이 늘어남  

### Autoregressive model
* 특정 과거 시점 이후의 데이터만 고려한다
### Markov model
* Markov Chain role에 의하여 바로 전 state가 이전시점의 모든 데이터를 가지고 있다고 가정한다
* 위의 이유로 바로 전 시점의 데이터만 고려함
* 강화학습에서 많이 사용하는데 현실에 직접 적용하기에는 버려지는 정보량이 너무 많다

### Latent autoregressive model
* 과거의 모든 정보들을 요약한 hidden state를 사용한다
  * hidden state가 어떻게 정의되느냐에 따라서 모델간 많은 차이가 존재한다
* RNN도 Latent autoregressive model라고 볼 수 있다

***
## Recurrent Neural Network (RNN)
* 자기참조로 학습하는 네트워크

<center>

<img src="https://colah.github.io/posts/2015-08-Understanding-LSTMs/img/RNN-unrolled.png" alt="" width="500px"/>

</center>

* short-term dependencies
  * 먼 과거의 정보(Long-term)는 고려하기 힘들다
  * 자기참조로 인한 연산이 계속되면서 gradient vanishing(sigmoid, tanh)이나 exploring(ReLU 계열)이 발생한다

## Long Short Term Memory
* 먼 과거의 정보를 고려하기위해 고안된 RNN
* 기존에 존재하는 Hidden state에 내부에서만 연산되는 Cell State를 추가하여 먼 과거의 정보 또한 잘 기억할 수 있다

* $x$ : data
* $C$ : Cell state
* $h$ : hidden state
* $\sigma$ : sigmoid function
* $tanh$ : hyperbolic tan function

<center>

<img src="https://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-chain.png" alt="" width="500px"/>

</center>

### Cell state
* 먼 과거의 정보까지 요약해서 가지고 있다가 Hidden state에 넘겨주는 역할
* 과거의 정보가 희석되는것을 막는 Resnet의 Skip Connection과 비슷한 역할을 한다
* Cell state는 다음과 같은 과정으로 업데이트 된다
1. $t-1$시점의 Hidden state가 Forget Gate를 통과
   * Forget Gate : 중요하지 않은 정보들을 없애는 Gate
$$
f_{t} = \sigma(W_{f}\cdot\[h_{t-1}, x_{t}\] + b_f)
$$
2. $t-1$시점의 Hidden state가 Input Gate를 통과
   * Input Gate : Cell state에 저장해야하는 정보들을 결정하는 Gate
$$
\begin{aligned}
i_{t} &= \sigma(W_{i}\centerdot [h_{t-1}, x_{t}] + b_{f})\\\\
\tilde{C_{t}} &= tanh(W_{C}\cdot [h_{t-1}, x_{t} ]+b_{C})
\end{aligned}
$$ 
3. $t-1$시점의 Cell state와 Gate를 통해서 나온 값들의 연산으로 Cell state를 업데이트 한다  
$$
C_{t} = f_{t} * C_{t-1} + i_{t}*\tilde{C_{t}}
$$

### Hidden state
* 기존의 RNN에 Hidden state와 동일한 역할
* 아래의 Output Gate에 Cell state와 Hidden state의 연산으로 업데이트 된다
1. Output Gate
$$
o_t = \sigma(W_o [h_{t-1}, x_t] + b_i)\\\\
h_t = o_t * tanh(C_t)
$$


## Gated Recurrent Unit (GRU)
* LSTM과 비슷한 형태
* 2개의 Gate(reset Gate, update Gate)가 존재하고 Cell state가 없다
* LSTM보다 더 적은 parameter를 가진다  

<center>

<img src="https://user-images.githubusercontent.com/38639633/106863078-5d25ed80-670b-11eb-8be1-f0f0fc785874.png" alt="" width="300px"/>

</center>

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [colah.github.io - RNN image](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)