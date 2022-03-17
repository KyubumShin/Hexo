---
title: 부스트 캠프 ai tech 3주 1일차 Data 시각화 (2)
date: 2022-02-03 10:34:45
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
## 3. matplot.pyplot 기초
* 이 글에서는 python 시각화 라이브러리 matplot에 대해서 다루어 본다
* 기본적으로 가장 많이 사용하는 matplot.pyplot을 이용하여 그래프를 그린다.  

### **들어가기전에**
   * 보통 아래와 같이 많이 pyplot을 plt로 선언 한다  

```python
import numpy as np
import matplotlib.pyplot as plt
```

### **Figure & Axes**
* plt.figure로 그래프틀을 선언하고, plt.show()를 이용하여 화면에 나타낼 수 있다.  

> * num : figure의 id를 지정한다. 이미 지정한 id가 존재하고 그것이 다시 정의될 경우에 원래 존재하던 figure를 반환한다
> * figsize : 그래프틀의 크기를 지정한다
> * dpi : 해상도를 설정한다
> * facecolor : 배경화면의 색을 지정한다
> * edgecolor : 가장자리 라인의 색을 지정한다  

```python
fig = plt.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None)
plt.show()
==========
output
<Figure size 432x288 with 0 Axes>
```

* 위의 코드에 Axes라는 subplot을 추가해야지만 제대로 그래프가 나온다
* figure의 add_subplot()을 이용하여 Axes를 지정할 수 있다  

```python
fig = plt.figure()
ax = fig.add_subplot()
plt.show()
```

<center>

<img src="/img/viz2.PNG" alt="viz2" width="300px"/>

</center>

### **subplot**
* Axes에 추가적인 Argument 입력을 통해서 위치를 지정해 줄 수 있다.  
* suplots를 이용하여 fig와 Axes들을 동시에 정의 할 수도 있다.  

```python
fig = plt.figure()
ax1 = fig.add_subplot(1, 2, 1)
ax2 = fig.add_subplot(1, 2, 2)
plt.show()
```

<center>

<img src="/img/viz3.PNG" alt="subplot" width="300px"/>

</center>

### **plot**
* plot을 통해서 그래프를 그릴 수 있다.
* x축과 y축의 수치가 1대1 대응으로 그래프가 그려진다.
* figure, subplot에 plot을 통해 입력이 가능하다
* 여러번 plot을 할 경우 여러개의 그래프가 그려진다  
* 직접 색을 입력해서 그래프의 색상을 지정 할 수 있다

> * x : x축이 될 데이터들
> * y : y축이 될 데이터들

```python
fig = plt.figure()
ax1 = fig.add_subplot(1, 1, 1)
ax1.plot([1, 2], [1, 3], color = 'forestgreen')
ax1.plot([2, 3], [3, 1], color = 'r')
plt.show()
```

<center>

<img src="/img/viz4.PNG" alt="plot" width="400px"/>

</center>

### **text**
* label : 그래프에 label을 붙일 수 있다.
* 단 label을 표시하기 위해서는 legend()를 이용해야 한다.  

```python
fig = plt.figure()
ax1 = fig.add_subplot(1, 1, 1)
ax1.plot([1, 2], [1, 3], color = 'forestgreen', label = '1')
ax1.plot([2, 3], [3, 1], color = 'r', label = '2')
ax1.legend() # 이게 없으면 label 표시가 나오지 않음
plt.show()
```

<center>

<img src="/img/viz5.PNG" alt="plot" width="400px"/>

</center>

* 여러 메소드를 이용하여 그래프의 특정부분을 변경 시킬 수 있다.
* set_title : title을 지정할 수 있다.
* set_xticks : x축의 범주값을 지정할 수 있다.
* set_ticklabels : x축을 텍스트 값으로 지정할 수 있다.
* annotate : 그래프에 여러가지를 추가 할 수 있다.
* 여러 메소드의 자세한 내용들은 추후에 다룰 예정이다.

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)