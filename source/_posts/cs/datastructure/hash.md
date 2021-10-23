---
layout: drafts
title: Hash Table
tags:
- cs
- 자료구조
categories:
- Computer Science
- 자료구조
date: 2021-09-27 23:13:16
---


# Hash Table
## 1. Hash Table이란
해시 테이블은 (Key,value)를 기반으로 데이터를 저장하는 자료구조중 하나이다.  
해시테이블은 아래의 그림과 같이 Key값을 Hash 함수를 이용하여 고유한 index값으로 변환하고, 이 index에 해당되는 배열(bucket)의 위치에 저장한다. 이런한 구조로 인해 Key값에 Hash 함수를 수행하기만 하면 value값이 저장되어있는 Index를 얻는것이 가능하기 때문에 탐색에 O(1)의 시간복잡도가 소요된다.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/315px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)  

## 2. Hash Functions
Hash 함수는 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수이다. 
Hash Table에서는 Hash 함수를 이용하여 Key에서 부터 고유한 index를 얻는다. 아래에는 간단한 Hash 함수들을 나열해 보았다. 

* Division Method : 가장 간단한 Hash함수중 하나로 Key값을 Bucket의 사이즈로 나누어서 계산한다.
* Digit Folding : Key의 문자를 ASCII 코드로 바꿔 합한 데이터를 테이블 주소로 사용한다. 
* Multiplication Method : 

## 3. Hash Collapse
Hash 함수에 서로 다른 입력값을 넣었지만 같은 출력값이 나올경우 발생할 수 있는 상황을 말한다. 이러한 상황이 발생할때 해결방법으로 아래와같은 충돌 처리기법이 존재한다.

## 3.1 충돌 처리 기법
* Open Hashging : 주소 밖의 메모리에 저장
  * Chaining : 충돌이 발생하면 해당 주소에 linked list 이용해서 연결해 저장하는 방법
    * 데이터를 찾을시에 순차탐색을 해야하는 단점이 생김
* Close hashing(Open Addressing) : 테이블 내의 새로운 주소를 탐색하여 데이터를 입력하는 방식
  * Linear probing : 충돌이 발생할때마다 고정값만큼 이동한 주소에 저장하는 방법
  * Quadratic probing : 충돌이 발생한 만큼의 제곱값을 폭으로 주소에 저장하는 방법
  * Double hashing : 해시된 값을 한번더 해싱하여 새로운 주소를 할당하는 방법


## reference
http://www.laurentluce.com/posts/python-dictionary-implementation/