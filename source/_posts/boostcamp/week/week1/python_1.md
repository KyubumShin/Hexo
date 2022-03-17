---
title: 부스트 캠프 ai tech 1주 1일차 Python Basic for AI (1)
date: 2022-01-17 18:46:31
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 1. Python의 특징
  * **독립적인 플랫폼**  
    운영체제에 상관없이 작동하는 언어이다.
  * **인터프리터 언어**  
    별도의 컴파일링 없이 컴퓨터가 바로 처리할 수 있는 언어이다. 속도는 컴파일러 언어에 비해서 느리지만 메모리가 적게 필요하다.
  * **객체지향적**  
    실행 순서가 아닌 단위 모듈 중심으로 프로그램이 작성된다.
  * **Dynamic Typing 언어**  
    프로그램이 실행하는 시점에 프로그램이 사용해야하는 데이터 타입이 결정된다.

## 2. 변수
* **데이터를 저장하기 위한 메모리 공간**  
    변수가 정의되면 변수는 메모리 주소를 할당 받고, 그 메모리 위치에 값을 저장한다. 그 외에 python에서 어떻게 변수를 할당받고 메모리를 관리하는지 알고싶으면 아래의 영상을 참고하는걸 추천한다.  
  * https://www.youtube.com/watch?v=arxWaw-E8QQ
* **기본 자료형들은 +, -, \*, %의 사칙연산이 가능 하다**
* **Dynamic Typing을 지원하기 때문에 정의할 때에 자료형을 특정하지 않아도 된다.**
  * 실행하는 시점에서 변수형을 확인하고 결정하기 때문에 타 언어보다 속도가 느리다.
  * 아래와 같이 자료형간 형 변환또한 가능하다.  

```python
a = 1 # int형으로 정의
int(a) # int() 로 형 변환 가능  
str(a) # str로 재정의 이때의 값은 '5'
float(a) # float형으로 재정의 이때의 값은 '5.0'
bool(a) # boolean 형으로 재정이 이때의 값은 True
```

## 3. 리스트
* **여러 데이터들을 묶어서 표현할 수 있는 자료형**
* **python 에서는 리스트 내부에 여러가지 자료형이 동시에 존재할 수 있다.**  

### 1. List Indexing & Slicing
* Indexing : 리스트에 있는 값들은 주소를 사용해 호출이 가능하다
* index를 넣는 곳에 음수값을 넣어서 뒤에서부터 호출 할 수 있다.
* len(object_name) : object의 길이를 반환한다
```python
color = ['red', 'blue', 'green']
print(colors[0]) # red
print(colors[-1]) # green
print(len(colors)) # 3
color[0] = 'Yellow' # ['Yellow', 'blue', 'green']

```
* Slicing : list의 값들을 잘라서 부분적으로 표현할 수 있다.
* index과 같이 음수값 통해 역순으로도 가능하다.  

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(numbers[0:6]) # [1, 2, 3, 4, 5, 6] index 0번부터 6개
print(numbers[:]) # [1, 2, 3, ... , 7, 8, 9] 처음부터 끝까지
print(numbers[::2]) # [1, 3, 5, 7, 9] 2칸단위로 슬라이싱
print(numbers[-5::-1]) # [6, 5, 4, 3, 2, 1] 뒤에서 5번째부터 역순으로 슬라이싱
```

### 2. List 연산
* \+ : 두 리스트를 합쳐준다  
* \* : 리스트를 n회 반복해서 늘린다  
```python
num1 = [1, 2, 3]
num2 = [3, 4, 5]
num1 + num2 # [1, 2, 3, 3, 4, 5]
num1 * 2 # [1, 2, 3, 1, 2, 3]
```
* list.append(element) : list에 element를 추가한다
* list.extend(iterable) : list에 iterable의 원소들을 추가한다
* list.insert(index, element) : list의 특정 index 위치에 element를 삽입한다
* list.remove(element) : list의 특정 element를 삭제한다

```python
num = [1, 2, 3]
num.append([4, 5]) # [1, 2, 3, [4, 5]]
num.extend([1, 2]) # [1, 2, 3, [4, 5], 1, 2]
num.insert(0, 'a') # ['a', 1, 2, 3, [4, 5], 1, 2]
num.remove(1) # ['a', 2, 3, [4, 5], 2]
```

### 3. 2-dim list
* **행렬**
* **기존의 리스트와 비슷하지만, 복사할때 주의할점이 필요하다**  
  리스트를 복사할때 리스트 주소가 복사되기 때문에 내부의 리스트는 동일한 주소의 값을 가져 하나의 리스트를 변경하면 다른 리스트값도 변경됨  
  * python 모듈중 copy의 deepcopy를 이용하여 복사
```python
mat = [[1, 2, 3], [4, 5, 6]]
mat2 = mat
mat[1][0] = 2 # [[2, 2, 3], [4, 5, 6]]
mat2 # [[2, 2, 3], [4, 5, 6]]
```