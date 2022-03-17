---
title: 부스트 캠프 ai tech 3주 1일차 Data 시각화 (3)
date: 2022-02-03 12:06:00
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
## Barplot
* 직사각형의 막대를 사용하여 데이터를 표현하는 그래프
* category에 따른 수치값을 비교하기에 적합하다

### 1. 기본적인 Barplot
* barplot은 기본적으로 bar, barh가 존재한다.
* bar는 수직, barh는 수평으로 막대를 그린다

```python
fig, ax = plt.subplots(1, 2, figsize=(12, 7))
x = list('ABCDE')
y = np.array([1, 2, 3, 4, 5])
ax[0].bar(x, y)
ax[1].barh(x, y)
plt.show()
```

<center>

<img src="/img/bar1.PNG" alt="subplot" width="500px"/>

</center>

### 2. 다양한 Barplot 기법
* 다양한 barplot에 대해서 이야기를 할 예정이다
* 사용하는 데이터는 Boostcamp에서 제공한 데이터를 사용하였다
* Multiple
   * plot을 여러개 그리는 방법이다.
   * subplots의 sharey를 이용하여 y축의 범위를 공유할 수 있다.
   * 각 group의 분포를 알기 좋지만 group간 비교하기에는 쉽지 않다

```python
fig, ax = plt.subplots(1, 2, figsize=(12, 6), sharey=True)
ax[0].bar(group['male'].index, group['male'], color='royalblue')
ax[1].bar(group['female'].index, group['female'], color='tomato')
plt.show()
```

<center>

<img src="/img/bar2.PNG" alt="subplot" width="500px"/>

</center>

* Stack
   * 2개 이상의 그룹을 쌓아서 표현하는 방식이다
   * 맨 밑 group의 분포는 파악하기 쉽지만 그외는 파악하기 힘들다
   * bottom : bar의 시작 y좌표를 설정 할 수 있다.  

```python
fig, axes = plt.subplots(1, 2, figsize=(15, 7))
group_cnt = student['race/ethnicity'].value_counts().sort_index()
axes[0].bar(group_cnt.index, group_cnt, color='darkgray')
axes[1].bar(group['male'].index, group['male'], color='royalblue')
axes[1].bar(group['female'].index, group['female'], bottom=group['male'], color='tomato') # 각 category의 y축 시작지점을 group['male']의 수치로 지정한다
for ax in axes:
    ax.set_ylim(0, 350)
plt.show()
```

<center>

<img src="/img/bar3.PNG" alt="subplot" width="500px"/>

</center>

* Percentage Stack
  * Stack을 응용하여 만든 BarPlot
  * bal_label을 이용하여 중간에 퍼센트를 찍어주었다  

```python
fig, ax = plt.subplots(1, 1, figsize=(12, 7))

group = group.sort_index(ascending=False) # 역순 정렬
total=group['male']+group['female'] # 각 그룹별 합

for name, color in zip(['male', 'female'], ['royalblue', 'tomato']):
    rects = ax.barh(group[name].index, group[name]/total, 
            left=group['male']/total if name == 'female' else 0, 
            color=color)
    ax.bar_label(rects, fmt='%.2g', label_type='center')

ax.set_xlim(0, 1)
for s in ['top', 'bottom', 'left', 'right']:
    ax.spines[s].set_visible(False)

plt.show()
```

<center>

<img src="/img/bar4.PNG" alt="subplot" width="400px"/>

</center>

* Overlap
  * 2개의 그룹만 비교할때 사용하기 좋은 방식
    * 3개 이상은 파악이 어렵다
  * 같은 축을 사용하기 때문에 비교하기 쉽다
  * Bar보다는 Area에서 더 효과적이다

```python
group = group.sort_index()
fig, axes = plt.subplots(1, 1, figsize=(8, 6))

axes.bar(group['male'].index, group['male'], 
        color='royalblue', 
        alpha=0.7)
axes.bar(group['female'].index, group['female'],
        color='tomato',
        alpha=0.7)
ax.set_ylim(0, 200)
plt.show()
```

<center>

<img src="/img/bar5.PNG" alt="subplot" width="400px"/>

</center>


* Group
  * 그룹별 범주에 따른 막대를 이웃되게 배치하는 방법
  * Matplotlib로는 구현이 까다롭다
  * 그룹이 5~7개 이하일때 효과적이다
    * 많으면 오히려 역효과가 난다


### **`시각화시 주의해야할점`**
1. 실제값과 그래픽으로 표현되는 부분은 비례해야한다
   * 반드시 x축의 시작은 0부터 한다
   * 차이를 나타내고 싶다면 세로의 비율을 늘리자
2. 정확한 정보를 전달하기 위해서 정렬을 하자
   * 데이터의 종류에따라 여러 기준으로 정렬을 한다.
   * 시계열 : 시간
   * 수치형 : 크기
   * 순서형 : 범주의 순서대로
   * 명목형 : 범주의 값에 따라서
   * interactive로 제공하는 것이 유용하다
3. 여백을 잘 조절하자
   * 너무 꽉차있거나 비어있으면 가독성이 떨어진다. 적절한 조절로 가독성을 높이자
   * .set_xlim(), .set_ylim()으로 표시할 영역을 지정한다
   * .spines[pos].set_visible()을 이용해서 외곽선을 안보이게 조절한다
   * Gap, Margins을 이용해서 적절히 간격을 띄운다
4. 복잡함을 줄이자
   * 3D는 왠만해서는 쓰지말자...
   * 축과 디테일을 조절하여 가독성과 깔끔함을 동시에 챙기자
     * text, annotate등을 이용하자


### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)