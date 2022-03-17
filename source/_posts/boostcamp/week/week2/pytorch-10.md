---
title: 부스트 캠프 ai tech 2주 4일차 Pytorch (8)
date: 2022-01-27 15:34:38
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
### Pytorch Troubleshooting
* OOM : Out Of Memory
  * GPU의 메모리가 터질때 발생하는 현상...
  * 왜 발생했는지 알기힘듬
  * 메모리의 이전상황의 파악이 어려움
* OOM의 해결방법
  * 보통 이 아래방법으로 대부분 해결된다
  * Batchsize를 줄여서 메모리 부하를 줄인다
  * torch.cuda.empty_cache()를 이용하여 GPU의 메모리를 clear 한 뒤에 학습시킨다
* 그 외에 신경쓰면 좋을점
  * GPUtil Module 사용하기
  * tensor.no_grad() 사용하기
  * 적절하게 del 명령어 사용하기
  * 다양한 batchsize로 돌려서 가능한 batchsize 알아보기
  * tensor의 float 32를 float 16으로 줄여보기

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)