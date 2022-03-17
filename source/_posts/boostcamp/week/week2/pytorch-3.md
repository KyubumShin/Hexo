---
title: 부스트 캠프 ai tech 2주 2일차 Pytorch (3)
date: 2022-01-24 15:30:11
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
## 3. **torch.nn**
* Pytorch의 Nerual Network와 관련된 기능들이 있는 모듈이다
* Neural Network와 관련된 Layer, Function들이 속해있다
  * Layer : 1층의 인공신경망을 이야기한다. input으로 들어온 값을 선형연산이나, 비선형연산을 통해 output을 return해 주는 class이다
  * Function : 활성화함수 등의 Neural Network의 연산을 하기위해 필요한 함수을 이야기한다  

### 3.1 **nn.Module**
* Custom Network(모델)를 만들기 위해서 지원하는 module이다
* nn.Module은 내부에 Module을 포함할 수 있다
  * 여러층으로 쌓이는 모양으로 인해 Layer라고도 부른다
  * Layer가 모여서 Model을 이룬다
* 기본적으로 아래와 같은코드를 베이스로 만들 수 있다
  * super : nn.Module에서 Attribute를 상속받기위한 선언. 이것이 없으면 빈 깡통 클래스이다
  * forward : 순전파를 구현하는 함수  
```python
class TestNet(nn.Module):
    def __init__(self):
        super(TestNet, self).__init__()

    def forward(self, x):
        return x_out
```

### 3.2 **Container**
* Layer들을 묶어서 보관하기 위한 저장소
* [Containers  - PyTorch 공식 문서](https://pytorch.org/docs/stable/nn.html#containers)
1. nn.Sequential()
   * 여러 모듈을 하나로 묶어서 하나의 모듈처럼 사용할 수 있는 Container
   * 순차적인 Layer들을 하나로 묶어서 깔끔하게 관리 할 수 있다
2. nn.ModuleList()
   * 여러 모듈을 list처럼 한군데 모아두는 Container
   * indexing을 통해 필요한 모듈을 꺼내 쓸 수 있다
   * 일반적인 List와 다르게 Attribute여도 Class를 print할 때 외부에 출력된다
3. nn.ModuleDict()
   * 여러 모듈을 dict처럼 한군데 모아두는 Container
   * Key값을 통해 필요한 모듈을 불러올 수 있다
   * ModuleList()와 같이 Class를 print할 때 외부에 출력된다  

### 3.3 **Parameter & Buffer**
* Parameter
  * 모듈안에 임시로 저장되는 특별한 Tensor
  * 일반적인 Tensor attribute와는 다르게 기울기 계산이 가능하고, 모델저장시에 같이 저장된다
  * RNN 같이 parameter가 반복되고, 갱신이 필요한 경우 사용된다
  * 또한 모듈속의 내부모듈들의 tensor는 전부 parameter로 지정된다
  * Parameter()로 선언 할 수 있다
* Buffer
  * 모듈안에 임시로 저장되는 Tensor
  * 모델저장시에 같이 저장된다
  * config용의 정보등을 저장할 때 사용한다
  * nn.Module의 register_buffer로 등록할 수 있다

### 3.4 **Module 내부 살펴보기**
* nn.module에는 내부의 여러 attribute를 볼 수 있는 기능이 존재한다
* 내부의 모듈, Parameter, buffer 등 여러 attribute가 ObjectDict형태로 저장되어 불러올 수 있다
1. submodule
   * 모듈속 모듈인 submodule은 아래의 함수들로 살펴 볼 수 있다
   * named_children
     * module에 바로 아래단계에 속한 submodule만 보여준다
   * named_modules
     * submodule 뿐만아니라 module에 속해있는 모든 module을 보여준다
2. parameter
   * named_parameters를 통해 parameter를 호출이 가능하다
3. buffer
   * named_buffers를 통해 buffer 호출이 가능하다

### 3.5 **hook**
* package화 된 코드에서 custom 코드를 중간에 실행시킬 수 있도록 만들어 놓은 인터페이스
* pytorch에는 등록하는 대상에 따른 2가지 종류의 hook
  * Tensor에 등록하는 Tensor hook
  * Module에 등록하는 Module hook  
* 실행 시점에 따른 5가지 종류의 hook이 존재한다
  * forward pre hooks : forward 연산 전에 실행되는 hook
  * forward hooks : forward 연산 후에 실행되는 hook
  * backward_hooks : backward 연산이 수행될때 마다 실행되는 hook. 현재는 사용하는걸 권장하지 않는다
  * full backward hooks : backward 연산이 수행될때 마다 실행되는 hook
  * state dict hooks : load_state_dict 함수가 모듈 내부에서 실행하는 hook, 직접적으로 user가 잘 사용하지는 않는다
1. **Tensor hook**
   * Tensor에 대한 Backward Propagation 후에 작동하는 hook
   * torch.Tensor.register_hook 을 통하여 hook을 등록 할 수 있다
   * torch.Tensor._backward_hooks 을 통하여 등록한 hook을 확인 할 수 있다
```python
def hook(grad):
  pass
tensor.register_hook(hook)
tensor_backward_hooks() # OrderedDict([(0, <function __main__.hook(grad)>)])
```
2. **Module hook**
   * Module hook은 3개의 종류의 hook으로 사용된다
   * forward pre hooks
   * forward hooks
   * ~~backward_hooks~~
   * full backward hooks
* forward pre hooks
  * forward 연산이 일어나기 전 시점에서 실행되는 hook
  * parameter로 module과 input으로 받고 input을 수정해서 return 할 수 있다
  * Module.register_forward_pre_hook(hook)으로 등록이 가능하다
```python
forward_pre_hook(module, input) -> None or modified input
```
* forward hooks
  * forward 연산이 일어난 뒤 시점에서 실행되는 hook
  * parameter로 module, input, output으로 받고, output을 수정해서 return 할 수 있다
  * input값또한 수정이 가능하지만 forward 연산에 변화는 없다
  * Module.register_forward_hook(hook)으로 등록이 가능하다
```python
forward_hook(module, input, output) -> None or modified output
```
* full backward hooks
  * backward 연산이 수행될때 마다 실행되는 hook
  * parameter로 module, grad_input, grad_output으로 받고, 새로운 grad_input return 할 수 있다
  * parameter인 grad_input 자체를 수정하면 Error가 발생할 수 있다
  * Module.register_full_backward_hook(hook)으로 등록이 가능하다  
```python
full_backward_hooks(module, grad_input, grad_output) -> None or modified grad_input
```

### 3.6 **apply**
* 특정 함수를 Module과 Module에 속한 submodule에 적용하는 함수
* weight 초기화나, 내부 모듈에 특정한 method를 추가할 때 사용할 수 있다
* weight_initialization
```python
def weight_initialization(module):
    module_name = module.__class__.__name__
    if 'Function' in module_name:
        module.W.data.fill_(1)
```
* make_method
```python
def function_repr(self):
    return f'name={self.name}'

def add_repr(module):
    module_name = module.__class__.__name__
    if 'Function' in module_name:
        module.extra_repr = partial(function_repr, module)
```
