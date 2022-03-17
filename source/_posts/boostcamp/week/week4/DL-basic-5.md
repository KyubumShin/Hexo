---
title: 부스트 캠프 ai tech 4주 3일차 DL Basic (5)
date: 2022-02-08 12:17:13
tags:
- DeepLearning
- week4
- CNN
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
### Fully Convolutional Network
* CNN에서 마지막을 담당하던 Dense Layer를 Dense Layer Feature와 동일한 Channel수를 가진 Convolution Layer로 대체한 Network
* Dense Layer는 reshape을 통해서 input을 집어넣기 때문에 정해진 input size가 필요 했지만, convolution Layer의 경우 channel 이외에는 가변적이기 때문에 이미지의 크기와 상관없이 연산이 가능해졌다
* 연산을 할 때 마다 차원이 축소되는 문제가 있다 -> upsampling기법을 사용
  * conv transpose -> checker board
  * unpooling

## Object Detection
### R-CNN 계열
* R-CNN
  * Selective Search 로 BBox 2000개정도를 추출 한 뒤 각각 CNN을 돌린다
  * CNN 연산이 2000번 반복되기 때문에 매우 느린 속도이다
* fast R-CNN
  * SPP Net을 이용하여 기존 2000번 반복된 연산을 1번으로 줄임
* Faster R-CNN
  * Selective Search를 Region Proposal Network로 바꾼 R-CNN
  * Region Proposal Network : BBox도 네트워크 학습으로 뽑아내자
  * 기존에 존재하는 anchor Box(샘플한 여러 크기의 Bbox)와 이미지를 비교하여 물체가 있을법한 장소를 탐색하고, 대략적인 Bbox위치를 특정한다

### Yolo
* BBox와 Classfication이 동시에 이루어지는 1 stage 모델
* R-CNN 계열에 비해서 속도가 매우 빠르지만, 정확도는 조금 떨어진다
* 실시간 물체검출이나 추적에 용이한 모델이다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)