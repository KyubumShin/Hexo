---
title: 부스트 캠프 ai tech 2주 3일차 Pytorch (4)
date: 2022-01-26 10:50:44
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
## 4. **Dataset & DataLoader**
* pytorch에서 생성한 모델을 학습시키기 위해 데이터를 공급해주는 유틸리티

### 4.1 **Dataset**
* Data를 담고 있는 Class
* pytorch Dataset은 아래와 같이 3가지의 기본 Method로 구성되어있다
* \_\_init\_\_: 초기화 함수. 필요한 변수들을 선언하고, data를 load하는 부분이다
* \_\_len\_\_: 데이터의 개수를 반환하는 함수. Dataloader에서 길이등을 반환하는데 쓰인다
* \_\_get_item\_\_(index): index번째의 data를 반환하는 함수. tensor로 return 해준다.
* 데이터에 따라 Map style과 iterable style로 나뉜다
  * Map style : 일반적인 data 구조
  * iterable style : random으로 읽기 어렵거나 data에 따라 batchsize가 달라지는 data. 시계열 데이터 등에 적합하다
* Map style 코드는 아래와 같다  
```python
class BasicDataset(Dataset):
    def __init__(self, path):
        self.data = pd.read_csv(path)
        self.X = self.data.drop(['label'])
        self.y = self.data['label']
    
    def __get_item__(self, idx):
        return self.X.iloc[idx], self.y[idx]
    
    def __len__(self):
        return len(self.X)
```


### 4.2 **DataLoader**
* Dataset을 iterable 하게 사용할 수 있도록 도와주는 Utility
* data loading 순서 커스터마이징, 자동 batch 설정, Single-Multi process data loading등 여러가지 기능을 지원한다

```python
DataLoader(dataset, batch_size=1, shuffle=False, sampler=None,
           batch_sampler=None, num_workers=0, collate_fn=None,
           pin_memory=False, drop_last=False, timeout=0,
           worker_init_fn=None, *, prefetch_factor=2,
           persistent_workers=False)
```

1. dataset
   * `torch.utils.data.Dataset` parameter
2. batch_size 
   * Data를 불러올 때 배치사이즈를 설정하는 항목  
3. shuffle 
   * Data load 순서를 항상 랜덤하게 뽑을지를 결정하는 항목
   * torch.manual_seed 를 통해 랜덤값을 고정할 수도 있다  
4. sampler
   * Data의 index를 컨트롤 하는 방법
   * `torch.utils.data.Sampler` 객체를 사용한다
   * SequentialSampler : 항상 같은 순서로 elements들을 sampling한다
   * RandomSampler : 랜덤하게 sampling 한다. replacement 가능, random의 범위를 지정 가능하다 (default=len(dataset))
   * SubsetRandomSampler : 랜덤하게 sampling 한다 위의 두 기능은 없다
   * WeigthRandomSampler : 가중치에 따라 뽑히는 확률이 달라진다
   * BatchSampler : Batch단위로 sampling을 해준다
   * DistributedSampler : Multi GPU에서 분산처리를 할때 사용한다  
5. batch_sampler
   * sampler와 같지만 기본적으로 BatchSampler가 적용된 상태이다
6. num_workers 
   * GPU에 Data를 load 할때 사용할 process의 수를 결정한다
7. collate_fn 
   * sample list를 합쳐서 tensor의 minibatch로 바꿔주는 기능. map style의 dataset에서 사용한다
   * 데이터마다의 길이가 다른 NLP에서 많이 사용한다
8. pin_memory 
   * pin memory를 사용하여 GPU에 더 빠르게 data를 load하는 방법. 
   * 추가적인 메모리 자원이 필요하다. 보통 parallel 모델에서 많이 사용한다 
9.  drop_last 
    * Data의 전체 개수가 batchsize로 나누어 떨어지지 않을때 마지막 batch를 drop를 결정하는 parameter

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [[Pytorch] DataLoader parameter별 용도](https://subinium.github.io/pytorch-dataloader/)
* [Pytorch DataLoader 공식문서](https://pytorch.org/tutorials/beginner/basics/data_tutorial.html)