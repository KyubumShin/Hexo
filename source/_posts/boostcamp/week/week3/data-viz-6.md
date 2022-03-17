---
title: 부스트 캠프 ai tech 3주 2일차 Data 시각화 (6)
date: 2022-02-04 10:59:55
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
## Text
* 시각화에 적절한 Text는 시각적인것으로만 전달하기 힘든 설명을 추가하거나 잘못된 전달에서 생기는 오해를 방지 할 수 있다
* 하지만 과한 Text는 오히려 방해가 될 수 있으니 주의할 필요가 있다

### 1. Anatomy of a Figure
* Title : 그래프의 주제
* Label : 축에 해당되는 데이터 정보
* Tick Lable : 축의 grid의 스케일 정보
* Legend : 한 그래프에서 여러개의 데이터 분류를 위한 보조 정보
* Annotation : 그 외의 시각화를 위한 보조정보

```python
코드 추가 필요
```

### 2. Text Properties
1. font Components
   * family : 글씨체
   * size or fontsize : 사이즈
   * style or fontstyle : 스타일(기울임체 등등)
   * weight or fontweight : 두께
   * [matplot Docs Fonts Demo](https://matplotlib.org/stable/gallery/text_labels_and_annotations/fonts_demo.html)

2. Detail
   * color : 글씨의 색
   * linespacing : 줄간격
   * backgroundcolor : 배경색
   * alpha : 투명도
   * zorder : z축 순서
   * visible : 랜더 유무
3. 정렬
   * ha : horizontal alignment
   * va : vertical alignment
   * rotation : 가로로 적을지 세로로 적을지 설정
   * multialignment : 추가적인 정렬
4. 그 외 추가적인 항목
   * bbox설정을 통해 text에 box를 만들수 있다.
     * [Drawing fancy boxes](https://matplotlib.org/stable/gallery/shapes_and_collections/fancybox_demo.html)

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)