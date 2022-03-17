---
title: Week8 - Day 1~4 Review
date: 2022-03-11 00:28:14
tags:
- 일상
- week8
categories:
- [boostcamp, Dairy]
- [일상, TIL]
widgets: null
---
***
## 1. 1~4일간 한 것
* CV 트랙 강의 수강 완료
* 과제 완료
* 추천 시스템 청강 준비

## 2. 피어세션에서 한 것
* receptive field 에 관한 정리
  * Convolution Layer에서 한번에 받을 수 있는 영역의 크기
  * 이 영역이 클수록 한번에 볼 수 있는 정보의 크기 또한 커진다
    * 성능의 향상
* 과제 리뷰
  * 1번과제 Resnet 34 scratch 구현에서의 의문점에 관하여 토론
    * ReLU의 적용 시점에 따라서 성능이 갈리지 않나?
  * 가이드라인 코드에서는 ReLU를 Skip Connection과 합치기 전에 각각 적용함
  * 직접 만든 코드에서는 ReLU를 합친 output에 적용하였다
  * 성능은 직접만든 코드쪽이 월등하게 높은것으로 나타났다

## 3. 주말 할 일
* 다다음주 P-Stage를 대비하여 필요한 지식을 미리 찾아두고 공부해두기
* Kaggle 스터디 발표준비 

## 4. 하루 느낀점
* 팀원이 바뀌고 새로 그라운드 룰부터 많은것을 정하기위해 정말 많이 이야기했다
* 아직 바뀐지 얼마 지나지 않아서 조금은 어색한 느낌이 있다
* 금방 좋아지겠지

## 5. 미세한 팁
* functools.partial에서 keyword값으로 넣어주려면 변수를 맨 뒤로 빼야한다
* {% post_link tip/partial 'functools.partial에 관한 정리' %}