---
title: 부스트 캠프 ai tech 9주 2일차 Conditional Generative Model
date: 2022-03-14 10:15:18
tags:
- DeepLearning
- week9
- CV
- GAN
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Conditional Generative Model
* `사용자가 컨트롤이 가능한` Generative Model
* 서로 다른 두 도메인을 변화시켜주는 Task
* 통역모델, 음성의 고품질 전환, 요약모델 등 다양한 분야에서 응용가능하다

## Conditional GAN
랜덤으로 생성되는 Latent Noise z 만 받는 GAN과는 다르게 latent Noise z + Conditional Input이나, domain Data의 형식으로 받는다

<center>

<img src="/img/cgan.PNG" alt="" width="600px"/>

</center>

* CV 응용분야
  * Style Transfer
  * Super resolution
  * Colorization

### Super Resolution
* 해상도가 낮은 이미지를 높은 이미지로 변환시키는 Task

<center>

<img src="/img/SR.PNG" alt="" width="300px"/>

</center>

* Super Resolution을 위한 Naive Re


## Image Translation Model

### Pix2Pix
* Pair Data

### CycleGAN
* UnPaired Data

## Perceptiaul Loss
* GAN은 학습시키기 힘들다
* 다른방법은 없을까?
* High quality ouput을 위한 Loss

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)