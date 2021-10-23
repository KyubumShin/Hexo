---
title: 링크드 리스트
date: 2021-08-28 22:31:05
tags:
- cs
- 자료구조
categories:
- Computer Science
- 자료구조
---

## 링크드리스트
링크드 리스트는 각 노드가 데이터와 포인터를 가지고 연결되어 있는 방식으로 데이터를 저장하는 자료구조이다

### 장점
* 원소 추가와 제거가 쉬움 : 시간복잡도 $O(1)$
* list의 크기를 가변적으로 사용가능

### 단점
* 탐색에는 효율이 좋지 않음 : 특정위치 탐색에 걸리는 시간복잡도 $O(n)$

### 결론
* 가변적으로 자주 변하는 데이터에 사용하면 좋다

## 종류
* 단일 연결 리스트 : 단방향으로 포인터가 연결된 리스트
* 이중 연결 리스트 : 양방향으로 포인터가 연결된 리스트
* 순환 연결 리스트 : Head와 Tail의 노드가 연결되어 순환구조를 가지는 리스트

## 구현

양방향 리스트로 구현해 보았다.

1. 노드
   * 데이터를 담을 노드를 구현
```python
class Node:
    def __init__(self, Data):
        self.Data = Data
        self.prev = None
        self.next = None
```
2. 리스트
   * head와 tail은 더미데이터를 넣어주어서 고려할 사항을 줄여줌
```python
class linked_list:
    def __init__(self):
        dummy = Node(None)
        self.head = dummy
        self.tail = dummy
        self.current = dummy

    def add(self, data): # 새로운 노드를 추가
        newNode = Node(data)
        self.tail.next = newNode
        newNode.prev = self.tail
        self.tail = newNode
        self.current = newNode

    def delete(self): # 현재 활성화 노드를 삭제하고 리턴
        next_node, prev_node = self.current.next, self.current.prev
        if next_node != None:
            next_node.prev = prev_node
        prev_node.next = next_node
        return self.current
        
    def delete_n(self, n): # n번째 노드를 삭제하고 리턴
        current = self.head.next
        for _ in range(n-1):
            current = current.next
        
    def prev(self): # 활성화 노드를 prev로 이동
        self.current = self.current.prev

    def next(self): # 활성화 노드를 next로 이동
        self.current = self.current.next
```