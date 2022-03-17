---
title: 부스트 캠프 ai tech 1주 3일차 Python Basic for AI (8)
date: 2022-01-19 11:08:11
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 12. Module 모듈
* 작은 프로그램 조각  
  이 조각들을 모아서 하나의 큰 프로그램을 만든다
* 사용하는 이유 : **`다른 프로그램에서 사용하기가 편하다`**
  ~~편하면 무조건 해야지~~
* module == .py 파일
* import 문을 사용하여 같은폴더 내의 module 이나 package를 호출한다
* module을 호출하는 방법
  1. 별칭으로 호출
  2. 특정 함수 또는 클래스만 호출
  3. 모듈에 모든 함수또는 클래스를 호출  

```python
import numpy as np  # 1
from numpy import ndarray  # 2
from numpy import *  # 3
```
* python에는 수많은 Built-in Modules이 존재한다
  * random, tqdm, time, collection, heap, Math ...

## 13. package
* 다양한 모듈이 모여서 이루어진 코드 묶음
* 오픈소스들이 모두 패키지로 관리된다  
* 각 폴더별로 필요한 모듈을 구현하고, \_\_init\_\_.py를 구성한다
* 추후에 \_\_init\_\_.py 와 \_\_main\_\_.py 작성법에 관련되어 포스팅을 할 예정이다


<center>

![tree](/img/package.PNG)

</center>

