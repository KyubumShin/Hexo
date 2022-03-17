---
title: data-viz-5
date: 2022-02-04 10:45:45
tags:
categories:
widgets:
---
***
## scatterplot
* 점을 통해서 그리는 그래프
* 상관관계를 확인하기위해 그리는 그래프
* color, marker(모양), size으로 다양한 바리에이션을 주는것이 가능하다

### scatterplot에서 확인해할 것
* 군집을 판단한다
* 값의 차이를 확인한다
  * 빈공간을 데이터를 보고 어떻게 채울지
* 이상치를 파악하자
  * scatterplot을 통해서 이상치를 파악하고 처리할 수단을 생각한다

### Overplotting
* 점이 많아져서 분포를 파악하기 힘들 상황
  * 투명도 조절
  * jittering 점의 위치를 겹치지않게 변형
  * 2차원 히스토그램 : 히트맵으로 변화시켜서 시각화
  * Countor plot : 등고선으로 표현

### 점의 요소와 인지
* 색
  * 연속적인것은 gradient, 이산은 category color로
* marker
  * 구별하기가 힘들다
  * 크기가 고르지 않다
  * 색과 병행해서 사용하자
* 크기
  * 버블차트
  * 관계보다는 점간 비율에 초점을 두고 사용하자
  * 오용하기 쉽기때문에 조심할것!

### 인과관계와 상관관계
* 인과관계와 상관관계를 구별해서 사용하자
  * 상관관계가 보인다고해서 인과관계가 있는것이 아니다
* 항상 text를 추가해서 설명해주는것이 더 좋다

### 추세선
* 상관관계가 존재할 경우에는 추세선을 추가해서 정보를 더 제공할 수 있다.
* 대신 2개이상 사용하는것은 지양할것

### 그 외
* Grid는 지양하는게 좀 더 깔끔한 시각화를 제공한다
* Category data는 버블차트나 히트맵을 사용하는편이 좋다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)