---
title: 부스트 캠프 ai tech 4주 4일차 DL Basic (8)
date: 2022-02-09 11:38:34
tags:
- DeepLearning
- week4
- VAE
- Generative Model
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Generative Model
* 생성모델은 아래와 같은 특징을 가진다
* Generatation
  * 기존의 데이터 확률분포 $p(x)$ 에 속하는 $x_new$를 만들어 낸다
* Density estimation
  * data $x$가 기존의 데이터와 비슷하면 확률분포 $p(x)$상에 존재할 가능성이 높다.
  * anomaly detection 이상치 탐지
  * 설명 가능한 모델 등이 있다

## Variaty Autoencoder
* Latent Space로 부터 데이터를 생성해내는 모델을 말한다
* Encoder와 Decoder 2부분으로 이루어져 있다
  * Encoder에서는 기존의 Dataset으로 부터 Latent Space를 생성한다
    * $x \rightarrow p(x)$
  * Decoder는 Latent Space로부터 역으로 Data를 생성한다
    * $p(x) \rightarrow x$
* 그래서 Encoder에서는 Dataset으로 Latent Space의 확률분포를 근사하고
  * $q_\phi$(z|x)
* Decoder에서는 Latent Space에서 기존 Dataset의 확률분포로 이동을 시켜준다
  * $p_\theta(x)$
  * 하지만 위의 확률분포는 우리가 알 방법이 없다
* 그래서 이것을 근사하기 위해 VAE에서 사용된 2가지 기법에 대해서 간략하게 설명한다

### Variaty Inference
* $q_\phi(z|x)$와 $p_\theta(z|x)$의 차이($D_{KL}$)를 줄이는것이 궁극적인 목표이다
  * 하지만 $p_\theta(z|x)$은 우리가 알 수가 없다
* 그래서 Maximum Likehood를 변형시켜서 학습에 이용한다

* $\mathcal{L}(\theta, \phi ; x)$ : Evidence Lower Bound (ELBO)
$$
\begin{aligned}
log(p_\theta (x)) &= \int_z q_\phi(z|x)log(p_\theta(x))\\\\
&= \mathcal{L}(\theta, \phi ; x) + D_{KL}(q_\phi(z|x)||p_\theta(z|x))
\end{aligned}
$$

* $D_{KL}$는 항상 1보다 크기때문에 위의 식은 다음과 같이 나타낼 수 있다.

$$
log(p_\theta (x)) \geq \mathcal{L}(\theta, \phi ; x)
$$

* 여기서 ELBO를 크게 하는 쪽으로 학습을 하게되면 $D_{KL}$은 줄어들게 된다.

### Reparametrization Trick
* 학습과정 중간에 Sampling이 들어가서 미분이 되지 않는것을 해결하기 위한 Trick
* sampling 한 값 $z$가 $\mu_q + \sigma_q \cdot \epsilon$ 과 같다고 생각하고 기존에 없던 $z$에 대해서 미분이 가능하게 바꾸었다.



### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [PR-[010] : Auto-Encoding variational Bayes ICLR 2014](https://www.youtube.com/watch?v=KYA-GEhObIs&list=PLlMkM4tgfjnJhhd4wn5aj8fVTYJwIpWkS)
* [VARIATIONAL-AUTOENCODER와 ELBO(EVIDENCE LOWER BOUND)](https://hugrypiggykim.com/2018/09/07/variational-autoencoder%EC%99%80-elboevidence-lower-bound/)