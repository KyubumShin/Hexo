---
title: 부스트 캠프 ai tech 2주 1일차 Pytorch (2)
date: 2022-01-24 10:42:40
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
## 2. **유용한 torch 함수들**
* torch의 내장함수들 중 자주 쓰일만한 녀석들의 정리글이다  
[pytorch 공식문서 - 링크](https://pytorch.org/docs/stable/torch.html#tensors)
1. Tensors
2. Creation Ops
3. indexing, Slicing, Joining, Mutating
4.

### 2.1 **Tensors**
1. is_*
   * 데이터 형태가 tensor인지 판단, tensor의 내부 데이터 등의 여러가지 판단을 하는 함수
```python
x = torch.tensor([0])
is_tensor(x) # True
is_nonzero(x) # False, input : single element tensor
``` 
2. torch.numel(x)
   * 전체 element가 몇개인지 출력하는 함수  
```python
a = torch.randn(1, 2, 3, 4, 5)
torch.numel(a) # 120
```

### 2.2 **Creation Ops**
1. torch.from_numpy
   * ndarray를 torch.Tensor로 바꾸는 함수
2. torch.zeros(size), empty(size), ones(size)
   * 0, 빈, 1로 이루어진 tensor를 size 형태로 생성하는 함수
   * numpy와 같은 기능을 한다
3. torch.zeros_like(tensor), empty_like(tensor), ones_like(tensor)
   * tensor의 size를 가진 0, 빈, 1로 이루어진 tensor를 생성하는 함수
   * numpy와 같은 기능을 한다
4. torch.arrange(start, end, step)
   * numpy의 arrange와 같은 기능을 하는 함수
   * start 부터 end 까지 step마다의 수를 가진 1D-tensor를 생성한다
5. torch.linspace(start, end, steps)
   * start에서 end의 구간의 길이를 steps개로 균등하게 나누는 1D-tensor를 생성한다
6. torch.full(size, fill_value), torch.full_like(tensor, fill_value)
   * fill_value로 채워진 tensor를 생성한다

### 2.3 **indexing, Slicing, Joining, Mutating 함수**
1. torch.index_select(input, dim, index)
   * 특정한 index에 위치한 데이터를 모아서 return 해주는 함수
```python
A = torch.Tensor([[1, 2], [3, 4]])
torch.index_select(A, 1, torch.tensor([0]))
===========================================
output:
tensor([[1.],
        [3.]])
```
2. torch.gather(input, dim, index)
   * 특정한 index들에 위치한 데이터를 모아서 return 해주는 함수
```python
t = torch.tensor([[1, 2], [3, 4]])
torch.gather(t, 1, torch.tensor([[0, 0], [1, 0]]))
==================================================
output:
tensor([[ 1,  1],
        [ 4,  3]])
==================================================
index calculate:
out[i][j][k] = input[index[i][j][k]][j][k]  # if dim == 0
out[i][j][k] = input[i][index[i][j][k]][k]  # if dim == 1
out[i][j][k] = input[i][j][index[i][j][k]]  # if dim == 2
```
3. torch.cat(tensors, dim) == torch.concat 
   * tensors들을 합치는 함수
   * 기준이 되는 dim을 제외하고 같은 shape를 가지고 있어야한다
```python
x = torch.rand(1, 3)
y = torch.rand(2, 3)
torch.cat((x,y), 0).size() # torch.Size([3, 3])
```
4. torch.chunk(input, chunks, dim)
   * tensor를 chunk의 갯수만큼으로 분리해주는 함수
   * chunks의 갯수가 넘어가지 않는 선에서 같은 size의 tensor로 분리해준다
   * 나누어 떨어지지 않는경우 마지막 tensor의 사이즈의 크기가 다를 수도 있다
```python
torch.arange(13).chunk(6)
=========================
output:
(tensor([0, 1, 2]),
 tensor([3, 4, 5]),
 tensor([6, 7, 8]),
 tensor([ 9, 10, 11]),
 tensor([12]))
```
```python
t = torch.tensor([[1, 2, 3],
                  [4, 5, 6]])
print(torch.chunk(t, 2, 1))
===========================
output:
(tensor([[1, 2],
        [4, 5]]), tensor([[3],
        [6]]))
```
5. torch.Tensor.scatter_(dim, index, src, reduce=None)
   * Tensor에 index에 맞춰서 src를 삽입하는 함수이다
   * reduce에 add, multiple을 넣어서 더하거나 곱하기도로 바꿀 수 있다
   * torch.gather와 반대로 작동한다
```python
src = torch.arange(1, 11).reshape((2, 5)) 
# tensor([[ 1,  2,  3,  4,  5], [ 6,  7,  8,  9, 10]])
index = torch.tensor([[0, 1, 2, 0]])
torch.zeros(3, 5, dtype=src.dtype).scatter_(0, index, src)
==========================================================
output:
tensor([[1, 0, 0, 4, 0],
        [0, 2, 0, 0, 0],
        [0, 0, 3, 0, 0]])
==========================================================
index calculate:
self[index[i][j][k]][j][k] = src[i][j][k]  # if dim == 0
self[i][index[i][j][k]][k] = src[i][j][k]  # if dim == 1
self[i][j][index[i][j][k]] = src[i][j][k]  # if dim == 2
```
6. torch.stack(tensors, dim)
   * 지정하는 차원으로 확장해서 tensor를 쌓아주는 함수이다
   * 두 차원이 정확하게 일치해야 쌓기가 가능하다
```python
x = torch.rand(3, 1, 3) # 3, 1, 3
y = torch.rand(3, 1, 3) # 3, 1, 3
torch.stack((x,y), dim=2).size() #torch.Size([3, 1, 2, 3])
```
### 2.4 **random Sampling**
* 자주 쓰이지만 numpy와 비슷해서 문서를 참고하는편이 좋을듯 하다
* [Random sampling - PyTorch 공식 문서](https://pytorch.org/docs/stable/torch.html#random-sampling)
* torch.seed(), torch.manual_seed(int)
   * Seed값을 고정해서 랜덤한 변수를 고정시킬 수 있다
   * manual_seed는 직접 시드값을 입력할 수 있다

### 2.5 **Pointwise Ops**
* 수학 연산과 관련된 기능을 포함하는 함수군
  * numpy와 비슷하다
1. torch.sqrt(tensor)
   * 각 tensor의 element에 대한 제곱근을 구해주는 함수
2. torch.exp(tensor)
   * 각 tensor의 element에 대한 $e^x$
3. torch.pow(tensor)
   * 각 tensor의 element에 대한 $x^2$  

### 2.6 **Reduction Ops**
* 조건에 따라 특정한 tensor의 값을 가져오는 함수군
* 대부분 numpy와 동일하게 작동한다  
* [Reduction Ops - PyTorch 공식 문서](https://pytorch.org/docs/stable/torch.html#reduction-ops)  


### 2.7 **Comparison Ops**
* 비교와 관련된 기능을 포함하고 있는 함수군
* [Comparison Ops - PyTorch 공식 문서](https://pytorch.org/docs/stable/torch.html#comparison-ops)
1. torch.argsort(tensor)
   * tensor를 sort하는 index를 return 해준다
```python
a = torch.randint(1, 10, (3, 3))
a
torch.argsort(a)
================
output:
tensor([[9, 5, 3],
        [6, 4, 2],
        [5, 8, 6]])
tensor([[2, 1, 0],
        [2, 1, 0],
        [0, 2, 1]])
```
2. torch.eq, torch.gt, torch.ge
   * tensor의 값들이 같은지, 더 큰지, 이상인지를 판단하는 함수들이다

3. torch.allclose(input, other, trol, atol)
   * input tensor와 other의 원소들의 차가 특정 범위인지를 판단하는 함수
$$
|\operatorname{input} - \operatorname{other}| \leq atol + rtol \times|other|
$$

```python
torch.allclose(torch.tensor([10.1, 1e-9]), torch.tensor([10.0, 1e-08]))
# False
```

### 2.8 **Other Operations**
* 그 외 다양한 기능들이 모여있는 함수들
* [Other Operations - PyTorch 공식 문서](https://pytorch.org/docs/stable/torch.html#other-operations)
1. torch.einsum
   * Einstein Notation에 따라 연산을 진행하는 함수
   * Einstein Notation은 특정 index의 집합에 대한 합연산을 간결하게 표시하는 방법이다
```python
x = torch.randn(5)
y = torch.randn(4)
torch.einsum('i,j->ij', x, y)
============================
output:
tensor([[ 0.1156, -0.2897, -0.3918,  0.4963],
        [-0.3744,  0.9381,  1.2685, -1.6070],
        [ 0.7208, -1.8058, -2.4419,  3.0936],
        [ 0.1713, -0.4291, -0.5802,  0.7350],
        [ 0.5704, -1.4290, -1.9323,  2.4480]])
==============================================
As = torch.randn(3,2,5)
Bs = torch.randn(3,5,4)
torch.einsum('bij,bjk->bik', As, Bs)
====================================
output:
tensor([[[-1.0564, -1.5904,  3.2023,  3.1271],
        [-1.6706, -0.8097, -0.8025, -2.1183]],

        [[ 4.2239,  0.3107, -0.5756, -0.2354],
        [-1.4558, -0.3460,  1.5087, -0.8530]],

        [[ 2.8153,  1.8787, -4.3839, -1.2112],
        [ 0.3728, -2.1131,  0.0921,  0.8305]]])
```

### 2.9 **BLAS & LAPACK Ops**
* "BLAS" - Basic Linear Algebra Subprograms
* "LAPACK" - Linear Algebra PACKage
* 선형대수에 관련된 함수군이다
* [BLAS & LAPACK Ops - PyTorch 공식 문서](https://pytorch.org/docs/stable/torch.html#blas-and-lapack-operations)