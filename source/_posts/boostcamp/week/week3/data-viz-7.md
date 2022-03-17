---
title: 부스트 캠프 ai tech 3주 2일차 Data 시각화 (7)
date: 2022-02-04 13:54:53
tags:
- Data visualization
- week3
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## color
* 시각화에서 색을 통해서 효과적으로 채널을 구분할 수 있다
* 심미적인 요소 또한 시각화의 일부 요소이다
* 전달하고 싶은 내용을 깔끔하게 색을 통해서 전달하는것이 주 목표이다
  * 꼭 화려한것이 답은 아니다

## Color Palette

### 1. categorical color
* Discrete, Qualitative등의 다양한 이름으로 불린다
* 독립된 색상으로 구성되어 범주형 변수에 주로 사용된다
* 이산적인 개별값을 나타낼때 적합하다

<center>

<img src="https://betterfigures.files.wordpress.com/2015/06/categorical.png?w=500&h=250" alt="categorical" width="300px"/>

</center>

### 2. Sequential color
* 정렬된 값을 가지는 연속형 변수에 적합나다
* 연속적인 색상을 사용하여 표현한다
  * 어두운곳에서는 밝은색, 밝은 곳에서는 어두운색을 이용한다.
* 색상은 단일 색조로 표현하는것이 좋다.
* 대표적으로 github commit log의 색이 있다.

<center>

<img src="https://betterfigures.files.wordpress.com/2015/06/sequential.png" alt="subplot" width="300px"/>

</center>

### 3. Divergence color
* 연속형과 유사하지만 중앙을 기준으로 서로 다른색으로 나타난다
* 상반된 값을 표현하는데 좋다(기온, 지지율 등)

<center>

<img src="https://betterfigures.files.wordpress.com/2015/06/diverging.png?w=500&h=250" alt="subplot" width="300px"/>

</center>

## 그 외에 고려할 점
* 다름을 보이기 위한 `Highlighting`을 색으로 표현 할 수 있다.
* 보통 먼 색일수록 차이가 더 크게보이는 색상 대비를 사용한다.
* 색약이나 색맹을 가지는 읽는 사람을 위해 색 선택을 고려할 필요가 있다.

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [Sequential color](https://betterfigures.org/2015/06/23/picking-a-colour-scale-for-scientific-graphics/)