---
title: Week2 Homework
date: 2022-01-28 13:54:41
tags:
- week2
categories:
- [boostcamp, Problems]
widgets: null
mathjax: true
---
***
## 1. 기초과제
* 과제 내용
  * Pytorch의 Custom Model 제작에 필요한 nn.Module 함수들에 대한 공부
  * Dataset과 Dataloader의 구현
* 결과 및 회고
  * 평소 자주 쓰지 않았던 torch 함수들을 찾아보고 알게되는 기회가 되었다
  * 특히 hook과 apply같은 거의 보지 못했던 기능들이 나와 정리해 보았다
  * {% post_link boostcamp/week/week2/pytorch-3 'Pytorch nn.Module 관련 정리' %}
  * {% post_link boostcamp/week/week2/pytorch-5 'Pytorch Dataset & DataLoader 관련 정리' %}

## 2. 심화과제
* 과제내용
  * Transfer Learning과 weight 초기화 + Ray사용 해보기
* 결과 및 회고
  * Transfer Learning은 익히 알던 내용이여서 어렵지 않았다
  * weight 초기화를 할때 랜덤으로 초기화 해주는것보다 특정 initialization 을 진행하는것이 더 성능이 잘 나오는것에 대해 알게 되었다
    * 이미 pytorch에서는 layer별로 내부 Method에 적용되어있다고 한다
    * 자세한 내용은 kaiming_uniform_에 대해 찾아보는것을 추천한다
  * Ray는 코드 실행은 해보았지만 colab GPU 사용량 초과로 인해서 강제 종료 당했다
  * 추후에 Linux 환경의 컴퓨터에서 다시한번 실행을 해 볼 예정이다