---
title: 부스트 캠프 ai tech 1주 2일차 Python Basic for AI (5)
date: 2022-01-18 15:38:01
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 9. 데이터 구조
* Stack & Queue
* Tuple & Set
* Dictionary
* Collection

### 9.1 Stack & Queue
* Stack
  * 나중에 넣은 데이터를 먼저 반환하도록 설계된 데이터 구조
  * `LIFO` (Last in First Out)
  * 입력을 Push, 출력을 Pop이라고 한다
  * python의 list는 기본적으로 Stack의 구조를 가진다
* Queue
  * 먼저 넣은 데이터가 먼저 반환하도록 설계된 데이터 구조
  * `FIFO` (First in First Out)
  * 입력은 Push, 출력은 get 이라고 한다
  * 보통 python의 Dequeue를 사용한다.
* 정해진 크기를 넘어갈 경우 overflow, element가 없는데 반환을 시킬경우 underflow라고 한다.

### 9.2 Tuple & Set
* **`Tuple`**
  * `값의 변경이 불가능한 리스트`
  * index로 접근해서 값을 수정하는것을 막는다
  * 정의 할 때 ( )를 사용한다
  * 리스트와 동일하게 (+, *)연산, Indexing, Slicing을 사용한다
  * 사용자의 실수에 의한 에러를 사전에 방지하기 위해 변경할 필요가 없는 데이터를 저장할 때 사용한다  
  
```python
t = (1, ) # 값이 1개인 Tuple은 반드시 ,를 붙여야 함
t + t # (1, 1)
t[0] = 2 # Error 발생함
```
* **`Set`**
  * 값을 순서없이 저장, 중복을 허용하지 않는 자료형(확인필요)
  * set( )을 통하여 객체를 생성한다
  * set을 이용하여 다양한 집합연산이 가능하다
```python
s1 = set([1, 2, 3, 4, 5])
s2 = set([1, 3, 5, 7, 9])
s1.union(s2) # (1, 2, 3, 4, 5, 7, 9) 합집합
s1 | s2 # (1, 2, 3, 4, 5, 7, 9) 합집합
s1.intersection(s2) # (1, 3, 5) 교집합
s1 & s2 # (1, 3, 5) 교집합
s1.difference(s2) # (2, 4) 차집합
s1 - s2 # (2, 4) 차집합
```

### 9.3 Dictionary
* 데이터를 저장 할 때 구분지을수 있는 값(Key)를 함께 저장
* Hash 구조
* Key값을 활용하여 Value를 관리한다.
* dict( )나 { }로 객체를 생성한다

```python
number_dic = {'one': 1, 'two': 2, 'three': 3}
number_dic['one'] # 1, Key 값으로 value 출력 가능
country_code.items() # 데이터 출력
# dict_items([('one', 1), ('two', 2), ('three', 3)])
number_dic.keys() # key만 출력
# dict_keys(['one', 'two', 'three'])
number_dic.values() # value만 출력
# dict_values([1, 2, 3])
number_dic.get(1) # None, 아닐경우 None
number_dic.get('one') # 1, key가 존재할 경우 values 값을 return
```

### 9.4 Collections
* Python Built-in 확장 모듈
* 편의성, 실행 효율 등을 사용자에게 제공함
* 자주 사용되는 deque, difaultdict, Counter에 대해서만 다룰것이다
* `deque`
  * Stack과 Queue의 기능을 모두 지원하는 데이터 구조
  * List에 비해 효율적인 저장방식을 지원한다
    * popleft()등 삽입 삭제에 매우 효율적임
  * Linked List의 특성(rotate, reverse)을 지원한다
  * 기존 list 형태의 함수를 모두 지원함
```python
from collections import deque
q = deque()
q.append(a) # [a]
q.appendleft(b) # [b, a]
q.popleft() # [a]
```
* `defaultdict`
  * Dict type값에 기본값을 지정해서 key가 존재하지 않아도 기본값으로 찾아지는 기능을 가지고 있다
  * defaultdict(datatype) 으로 기본값의 자료형을 정하면서 dict객체를 생성할 수 있다
```python
from collections import defaultdict
dic = defaultdict(int)
dic['a'] += 1 # {'a': 1}
dic['b'] -= 1 # {'a': 1, 'b': -1}
```

* `Counter`
  * 시퀸스 type의 data element들의 갯수를 dict형태로 변환
```python
from collections import Counter
c = Counter([1, 3, 5, 3, 2, 4, 3])
# Counter({1: 1, 3: 3, 5: 1, 2: 1, 4: 1})
```