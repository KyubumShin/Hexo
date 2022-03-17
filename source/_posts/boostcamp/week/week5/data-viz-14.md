---
title: 부스트 캠프 ai tech 4주차 Data 시각화 (14)
date: 2022-02-16 11:02:15
tags:
- Data visualization
- week5
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Interactive Visualization

### 정형 데이터의 단점
* 각각의 데이터마다 plot해주어야 하기때문에 Feature가 많으면 그만큼 plot수도 많아진다
* 상관관계가 존재할 경우에는 10 * 9 개의 plot이 필요하다
* 공간적인 낭비가 크다
* 이러한 단점을 `Interactive한 시각화`로 보안할 수 있다

### Matplotlib
* 인터랙티브를 제공하지만 local에서만 가능
* 외부 라이브러리를 통해서 웹에도 서비스가 가능은 하다
* 기능또한 많지 않아서 의미가 크지 않다

### Plotly
* 가장 많이 사용하는 Interactive 시각화 라이브러리
* R이나 JavaScript같은 다른 언어도 지원한다
* 문서화가 잘되어있다
* 커스텀이 아쉽다

### Bokeh
* Matplotlib와 비슷한 라이브러리
* 문서화가 부족하다

### Altair
* 문법이 pythonic하지 않다
* 데이터 크기에 5000개의 제한이 있다
* 기본차트에 특화되어 있음



### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)