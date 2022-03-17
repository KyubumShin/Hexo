---
title: 부스트 캠프 ai tech 2주 1일차 Pytorch (1)
date: 2022-01-24 10:10:35
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
## 0. pytorch란?
* Meta(구 Facebook) 에서 개발한 딥러닝 프레임워크
* numpy + AutoGradient
* 동적 그래프 기반

## 1. pytorch 기본
* pytorch 에서는 Tensor class를 사용한다
* Tensor
  * numpy의 ndarray와 사실상 동일하다
    * 내장 함수도 대부분 비슷한 기능이 존재한다
  * tensor가 가질수 있는 type은 ndarray와 동일하나 GPU 사용이 가능한 차이가 존재한다  

### 1.1 기본 Tensor 함수
* list > tensor
```python
import torch
data = [[3, 5],[10, 5]]
x_data = torch.tensor(data)
##########################
output:
tensor([[ 3,  5],
        [10,  5]])
```
* ndArray > tensor
```python
nd_array_ex = np.array(data)
tensor_array = torch.from_numpy(nd_array_ex)
############################################
output:
tensor([[ 3,  5],
        [10,  5]])
```
* tensor > ndarray
```python
tensor_array.numpy()
####################
output:
array([[ 3,  5],
       [10,  5]])
```
* flatten
```python
data = [[3, 5, 20],[10, 5, 50], [1, 5, 10]]
x_data = torch.tensor(data)
x_data.flatten()
################
output:
tensor([ 3,  5, 20, 10,  5, 50,  1,  5, 10])
```
* one_like
```python
torch.ones_like(x_data)
#######################
output:
tensor([[1, 1, 1],
        [1, 1, 1],
        [1, 1, 1]])
```
* shape, dtype
```python
x_data.shape # torch.Size([3, 3])
x_data.dtype # torch.int64
```
* GPU load
```python
device = torch.device('cpu')
if torch.cuda.is_available():
    device = torch.device('cuda')
```

### 1.2 Tensor handling
* view & reshape
  * tensor의 shape를 변경하는 함수
  * view는 input tensor와 return tensor가 데이터를 공유하여 항상 같은 주소값들을 가진다
  * reshape은 tensor의 복사본 혹은 view를 반환한다
    * 원본과 동일한 tensor값이 필요할 경우에는 view를 사용하거나 clone()을 이용해야한다
* squeeze & unsqueeze
  * 차원의 개수가 1인 차원을 축소, 확장하는 함수
  * unsqueeze(index) : index에 1인 차원을 삽입해서 차원을 확장한다
```python
tensor_ex = torch.rand(size=(2, 1, 2))
tensor_ex.squeeze().shape # torch.Size([2, 2])
tensor_ex = torch.rand(size=(2, 2))
tensor_ex.unsqueeze(0).shape # torch.Size([1, 2, 2])
tensor_ex = torch.rand(size=(2, 2))
tensor_ex.unsqueeze(1).shape # torch.Size([2, 1, 2])
tensor_ex = torch.rand(size=(2, 2))
tensor_ex.unsqueeze(2).shape # torch.Size([2, 2, 1])
```

### 1.3 Tensor operation
* numpy와 동일하게 operation에 대해서 broadcasting을 지원한다
* 행렬곱셈 연산은 mm 및 matmul을 사용한다
  * dot은 1차원 벡터와 스칼라 연산에서만 사용가능
  * mm과 matmul은 2차원이상의 행렬연산에서만 사용가능
  * mm은 broadcasting을 지원하지 않지만 matmul은 지원한다

### 1.4 Tensor operation for ML/DL formula
* nn.functional을 이용한 다양한 연산가능
* softmax, argmax, one_hot 등등

### 1.5 AutoGrad
* 자동 미분
* tensor에 requires_grad=True로 설정해서 자동으로 gradient 추적이 가능하다
  * 기본적으로 nn모듈의 선형연산들은 default로 True로 설정되어있어 잘 쓰지 않는다
```python
tensor(data, requires_grad=True)
```
* backward() 함수를 통하여 Backpropagation 수행