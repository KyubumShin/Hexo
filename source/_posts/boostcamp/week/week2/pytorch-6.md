---
title: 부스트 캠프 ai tech 2주 3일차 Pytorch (5)
date: 2022-01-26 14:50:44
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
* 학습시킨 모델을 다른사람들에게 공유하거나, 보관하기 위에서는 메모리에 있는 Model들을 따로 파일로 만들어서 저장할 필요가 있는데 본 글에서는 저장을 어떻게 해야하는지, 그리고 이를 이용한 Tranfer Learning 에 대해서 다룰 예정이다  

## 5. Pytorch Model Save & Load 
* torch.save()
  * 학습의 결과를 저장하기 위한 함수이다
  * 모델의 Layer들과 Parameter, Buffer를 저장한다
  * 학습 중간중간 Model을 저장해서 최선의 성능을 가지는 결과모델을 선택하는 방식으로 사용 할 수 있다 (Checkpoint)
>* model : 학습한 모델
>* PATH : 모델을 저장할 directory
```python
# 모델의 weight 만 저장하는 방법
torch.save(model.state_dict(), PATH)
# 모델의 weight와 내부모듈 구조, Buffer까지 저장하는 방법
torch.save(model, PATH)
```
* checkpoints
  * 학습의 중간 결과를 저장해서 최선의 성능을 가지는 결과모델을 선택하는 방법
  * 보통 early stopping 기법과 함께 사용한다
    * early stopping : Loss와 Metric값을 지속적으로 확인 하면서 일정 기간이상 줄지 않으면 학습을 멈추는 방법
  * 일반적으로 epoch, loss, mertic을 함께 저장하여 확인한다  

```python
torch.save({
    'epoch': epoch,
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'loss': epoch_loss,
    }, f"saved/checkpoint_model_{epoch}_{epoch_loss/len(dataloader)}_{epoch_acc/len(dataloader)}.pt")

checkpoint = torch.load(PATH)
model.load_state_dict(checkpoint['model_state_dict'])
optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
epoch = checkpoint['epoch']
loss = checkpoint['loss']
```

## 6. Transfer Learning
* 다른 데이터셋으로 만든 모델을 현재 데이터셋에 맞춰서 다시 학습시키는 방법
  * 일반적으로 큰 데이터셋으로 학습시킨 모델(ex Imagenet 10K로 학습시킨 resnet50 등등)의 성능이 다른 데이터셋에 적용시키는것이 처음부터 학습하는 모델보다 학습이 빠르고, 학습이 잘된다
* 현재 DeepLearning에서 가장 일반적인 학습 방법이다
* 기존의 pretrained 된 모델을 backbone 모델이라고 하며 여기서 일부 Layer만 변경시켜서 학습을 수행한다
* CV : Pytorch 공식 비전 라이브러리 TorchVision 이나 torch image model(timm)을 많이 이용한다
* NLP : transformer 전문 라이브러리인 HuggingFace를 많이 사용한다

### 6.1 **Freezing**
* pretrained model을 활용할때 모델의 일부분을 freeze 시켜 파라미터의 업데이트가 일어나는것을 막는 방법
* DeepLearning의 특성상 학습이 계속 진행되면서 파라미터가 바뀌면 과거에 학습했던 정보가 희석되는 현상이 일어나는데 특히 pretrained 모델에게 안좋은 영향을 준다
* pytorch의 requires_grad를 비활성화 시키거나 hook를 이용해서 backward의 input_grad를 0으로 고정시켜버리는 것으로도 가능하다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)