---
title: 부스트 캠프 ai tech 3주 2일차 Data 시각화 (8)
date: 2022-02-04 15:00:16
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
## Facet
* 분할을 의미한다
* 화면상에 view를 분할하여 큰틀에서는 볼 수 없는 부분집합을 세세하게 보여줄 수 있다.

### 1. Figure & Axes
* Figure는 그래프가 들어가는 큰 틀, Axes는 각 plot이 들어가는 공간을 말한다.
* Figure는 항상 1개, Axes는 여러개가 존재할 수 있다.
* 아래의 함수들로 N by M 의 Axes(subplot)들을 만들 수 있다.
  * plt.subplot()
  * plt.figure() + fig.add_subplot()
  * plt.subplots()
* sharex, sharey를 통해 subplot끼리의 x축, y축의 범위를 통일 할 수 있다
* squeeze를 False로 지정해서 subplot의 index를 n by m Matrix로 바꿀 수 있다.
  * 기본으로 True이기 때문에 1차원 배열로 나오게 된다
* aspect을 통해서 눈금간의 간격의 길이를 설정 할 수 있다  

```python
fig = plt.figure(figsize=(12, 5))
ax1 = fig.add_subplot(121, aspect=1)
ax2 = fig.add_subplot(122, aspect=0.5)
plt.show()
```

<center>

<img src="/img/facet1.PNG" alt="" width="500px"/>

</center>


### 2. Grid spec
* css의 그리드 처럼 동일 크기 분할이 아닌 다양한 크기의 그래프를 그리고 싶을때 사용하는 방식이다
* add_subplot
  * numpy의 slicing과 비슷하게 사용이 가능하다  

```python
fig = plt.figure(figsize=(8, 5))
gs = fig.add_gridspec(3, 3)

ax = [None for _ in range(3)]

ax[0] = fig.add_subplot(gs[0, :2]) 
ax[0].set_title('gs[0, :]')

ax[1] = fig.add_subplot(gs[0:, -1])
ax[1].set_title('gs[0, -1]')

ax[2] = fig.add_subplot(gs[1:3, 0:2])
ax[2].set_title('gs[-1, 0]')

for ix in range(3):
    ax[ix].set_xticks([])
    ax[ix].set_yticks([])

plt.tight_layout()
plt.show()
```

<center>

<img src="/img/facet2.PNG" alt="" width="500px"/>

</center>

* subplot2grid((shape), (y, x), colspan = dx, rowspan = dy)
  * shape를 통해 그리고자하는 grid를 설정
  * y, x : 시작하고자하는 좌표값
  * colspan, rawspan : 할당하고자 하는 가로 세로 길이  

```python
fig = plt.figure(figsize=(8, 5))
ax = [None for _ in range(6)]

ax[0] = plt.subplot2grid((3,4), (0,0), colspan=4)
ax[1] = plt.subplot2grid((3,4), (1,0), colspan=2)
ax[2] = plt.subplot2grid((3,4), (1,2), colspan=1)
ax[3] = plt.subplot2grid((3,4), (1,3), colspan=1,rowspan=2)
ax[4] = plt.subplot2grid((3,4), (2,0), colspan=3)

for ix in range(5): 
    ax[ix].set_title('ax[{}]'.format(ix)) # make ax title for distinguish:)
    ax[ix].set_xticks([]) # to remove x ticks
    ax[ix].set_yticks([]) # to remove y ticks
    
fig.tight_layout()
plt.show()
```

<center>

<img src="/img/facet3.PNG" alt="" width="500px"/>

</center>

### 3. insert
* subplot 내부에 subplot을 생성하는 방법이다.
* ax.inset_axes()
  * Ax 내부에 subplot을 추가하는 방법
  * 메인 시각화를 해치지 않는 선에서 사용하자

```python
fig, ax = plt.subplots()

color=['royalblue', 'tomato']
ax.bar(['A', 'B'], [1, 2],
       color=color
      )

ax.margins(0.2)
axin = ax.inset_axes([0.8, 0.8, 0.2, 0.2])
axin.pie([1, 2], colors=color, 
         autopct='%1.0f%%')
plt.show()
```

<center>

<img src="/img/facet4.PNG" alt="" width="300px"/>

</center>

* make_axes_locatable(ax)
  * Ax 사이드에 부가적인 정보를 주는 방법
  * 보통 colorbar로 많이 사용한다  

```python
fig, ax = plt.subplots(1, 1)

# 이미지를 보여주는 시각화
# 2D 배열을 색으로 보여줌
im = ax.imshow(np.arange(100).reshape((10, 10)))

divider = make_axes_locatable(ax)
cax = divider.append_axes("right", size="5%", pad=0.05)

fig.colorbar(im, cax=cax)
plt.show()
```

<center>

<img src="/img/facet5.PNG" alt="" width="300px"/>

</center>

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)