---
title: 부스트 캠프 ai tech 2주 4일차 Pytorch (7)
date: 2022-01-27 13:36:25
tags:
- pytorch
- week2
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## 8. Hyperparameter Tuning
* Hyperparameter 란?
  * Learning Rate, Model의 inputsize, optimizer, loss function, batchsize 등의 모델이 스스로 학습하지 않는 값을 말한다
  * 이 Hyperparameter를 조절하여 성능을 올리는 방법을 Hyperparameter Tuning이라고 부른다
  * 생각보다 스펙타클하게 성능이 좋아지지는 않는다

### 8.1 Gradient Search
* parameter에 따른 기울기값을 계산한뒤 큰값을 내는(빠르게 학습이 가능한) parameter를 찾는 기법
* 보통 Learning rate를 찾는데 사용하는 기법이다
* 특정 간격마다의 값으로 검색하는 Grid Layout과 랜덤한 값으로 검색하는 Random Layout 등 여러가지 방법이 존재한다
* 최근에는 베이지안 기반의 기법들이 주도하고 있다
  * BOHB(Baysian Optimizer Hyperband)

### 8.2 Ray 라이브러리
* ML과 DL의 병렬 처리를 위해 개발된 모듈이다
* Hyperparameter Search를 위한 다양한 모듈을 제공한다
* ML과 DL을 위해 개발되긴 했는데 분산처리(Multiprocessing)코드를 단순하고, 범용적으로 작성할 수 있게 도와준다
* 병렬처리 양식으로 학습을 시행해서 성능이 좋지않은 process들을 제외해 가면서 최적의 hyperparameter를 찾는다
* 아래쪽의 참고 문서를 보는것을 추천한다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [Baysian Optimizer Hyperband](https://github.com/automl/HpBandSter)
* [BOHB: Robust and Efficient Hyperparameter Optimization at Scale
](https://arxiv.org/pdf/1807.01774.pdf)
* [Ray - github](https://github.com/ray-project/ray)
* [Python Ray 사용법 - Python 병렬처리, 분산처리](https://zzsza.github.io/mlops/2021/01/03/python-ray/)
* [HYPERPARAMETER TUNING WITH RAY TUNE](https://pytorch.org/tutorials/beginner/hyperparameter_tuning_tutorial.html)