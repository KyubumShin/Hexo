---
title: 부스트 캠프 ai tech 3주 1일차 Data 시각화 (4)
date: 2022-02-04 08:07:54
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
## Lineplot
* 연속적으로 변화하는 값을 점으로 나타내고 선으로 연결한 그래프

### 1. 기본적인 Lineplot
* .plot()으로 그래프를 그릴 수 있다
* 5개 이하의 선을 사용하는것이 가독성이 좋다
  * 색상, 마커, 선의 종류 등으로 선을 구분해서 가독성을 더 끌어 올릴 수 있다.
  * color : 색상 지정
  * marker : 점의 모양 지정
  * linestyle : 선의 종류 지정(solid, dashed, dashdot, dotted, None)
* 흐름의 파악을 원할하게 하기 위해 smoothing을 사용해서 Noise를 줄인다  
 
## 2. Lineplot의 특징

### 1. 흐름에 집중하는 그래프
* 데이터의 흐름을 보기위한 그래프이다
  * 그렇기에 bar와 다르게 축을 0에 맞출 필요는 없다
* 너무 구체적인 정보는 오히려 흐름을 보는데 방해 될 수 있다
  * Grid, Annotate등을 최소한으로 사용한다
  * 디테일한 정보는 따로 표로 제공하는것도 좋다
* 생략되지 않는 선에서 범위를 조절해서 표현한다
  * .set_ylim()을 이용하자

### 2. 간격
* 축의 간격이 다를경우 기울기 정보에서 오해를 일으킬 수 있다. 또한 점과 점 사이를 선으로 연결한 것이기 때문에 실제로 데이터가 없는부분에서 있다고 오해가 가능하다
  * 수치형 데이터일 경우 matplot에서 알아서 맞추어준다
  * 데이터의 위치에 mark를 해서 오해를 줄일 수 있다

### 3. 보간
* 점과 점사이를 실제 데이터가 없지만 이어서 선으로 만드는 방법
* 데이터의 error나 Noise가 포함되어 있을경우 보간을 사용해서 어느정도 보정해 이해를 도울 수 있다.
  * scipy모듈을 이용하여 사용
* 데이터를 분석할 경우 미세한 차이를 놓치거나, 없는데이터를 있다고 생각하게 할수 있기때문에 EDA에서는 지양하는것이 좋다.

### 4. 이중 축 사용
* 한 plot에 대해서 2개의 축을 사용하는 방법
* 같은 시간축에서 서로다른 데이터를 표현하기 위해서 쓴다.
  * .twinx()를 사용해서 구현한다
* 보통 한 데이터에 대한 다른단위 표현을 위해 사용한다
  * .secondary_xaxis(), .secondary_yaxis()를 사용한다
* 두 데이터에 대해서 이중 축을 사용하는것은 강제로 상관관계를 부여할 수 있으니 지양하고 2개의 plot을 사용하는쪽이 좀 더 가독성 면에서도 좋다


### 5.그 외 팁
* 라인 끝에 label을 추가하면 식별에 도움이 된다
* 주요 포인트에는 annotation을 추가하면 도움이 될 수도 있다
* 연한색으로 uncerainty 표현이 가능하다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)