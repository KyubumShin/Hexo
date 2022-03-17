---
title: 부스트 캠프 ai tech 4주 5일차 DL Basic (9)
date: 2022-02-09 11:38:46
tags:
- DeepLearning
- week4
- GAN
- Generative Model
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## GAN
* 적대적 생성모델
* 노이즈로부터 데이터를 생성하는 Generator와 데이터가 진짜 데이터인지 생성된 데이터인지를 판단하는 Discriminator 2개의 구조로 이루어져 있다
* Generator와 Discriminator는 서로의 Loss값을 최대로 하는 방향으로 학습을 하려 한다
  * Generator는 Discriminator의 판단한 결과로 실제 데이터와 유사하게 학습하는 방향으로 학습한다
  * Discriminator는 이진분류기로 실제데이터와 생성데이터를 분류한다

<center>

<img src="https://t1.daumcdn.net/cfile/tistory/9928E6375B75872D17" alt="" width="400px"/>

</center>
  
* GAN을 아래와 같이 표현이 가능하다.
$$
min_G\, max_D\, V(D,G) = \mathbf{E}_{x\sim p_{data}(x)}[\operatorname{log}D(x)] + \mathbf{E}_{z \sim p_{z}(z)}[\operatorname{log}(1 - D(G(z)))]
$$

## GAN & VAE
* VAE
  * 학습이 안정적이다
  * 결과물이 흐릿하게 나올 확률이 높다
  * 학습 데이터에 있는 데이터와 비슷하게 나온다
    * 새로운것을 만들어내지는 못함
* GAN  
  * 학습이 불안전하다
  * 출력물이 뚜렷한 편이다
    * 새로운 분포를 만들 수 있다
* 최근에는 VAE또한 많이 발전해서 output이 GAN 이상의 것들을 보여준다
### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)