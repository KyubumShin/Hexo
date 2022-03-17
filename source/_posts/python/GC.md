---
title: Garbage collection
date: 2022-02-02 16:48:22
tags:
- python
- week3
categories:
- Programming
- Python
widgets: Null
---
***
### **서론**
이 글에서는 Python의 Garbage Collector에 대해서 다룬다.

### **Garbage collection**
Garbage Collector(이하 GC)는 메모리 관리 기법중 하나로 동적으로 할당했던 메모리 영역 중에 필요없게 된 부분을 해제하는 기능이다. C, C++등의 언어들은 수동메모리 관리를 전재로 설계되어 malloc, free등의 함수로 직접 메모리를 관리 해주어야 하지만, Python, Java, C# 같은 고급 언어들은 GC가 내장되어 있어 자동으로 메모리 관리를 해준다.

### **Python GC의 작동방식**
Python의 GC는 reference count + Generational GC 방식으로 메모리를 관리한다.

**reference count**

```c
typedef struct _object {
    _PyObject_HEAD_EXTRA
    Py_ssize_t ob_refcnt;               /* reference count */
    struct _typeobject *ob_type;
} PyObject;
```

python의 객체들은 모두 reference count를 가지고 있으며 이것을 통해서 GC가 언제 메모리에서 제거할지를 판단한다. 참조가 이루어지면 reference count가 1증가하고, 참조가 끝나면 1감소한다. 최종적으로 0이 되면 GC에서 더이상 필요없는 오브젝트로 판단하고 메모리에서 삭제한다.  

이러한 방식은 프로그래머가 어느정도 오브젝트의 메모리 할당 해제 시점을 유추 할 수 있고, 대부분 사용된 직후 해제되기 때문에 캐시에 저장되어 있을 확률이 높아 빠르게 할당 해제가 이루어지는 장점이 존재한다.

하지만 아래와 같은 단점 또한 존재한다. 두개 이상의 객체가 서로 가리키고 있을 경우(순환 참조) reference count가 0까지 내려가지 않는 상황이 발생 할 수 있다. 또한 Multi Thread 환경에서는 공유자원에 대한 참조가 되기 때문에 추가적인 Lock 등이 필요하거나, 지속해서 GC에서 판단하는 프로세스를 거쳐야 하기 때문에 수행 성능의 저하 등의 문제가 발생 할 수 있다.

이러한 단점들을 해결하기 위해 Python에서는 순환 참조를 탐지하는 알고리즘과, 보조적인 Generational GC를 두었고, GIL로 Multi Threading에 제한을 걸어 버렸다.

**Generational GC**

새롭게 할당된 오브젝트일수록 금방 메모리에서 해제될 확률이 높다는 통계에서 기반한 메모리 관리방법이다. 각각의 오브젝트가 GC가 실행하고나서 메모리에서 해제되지 않으면 다음 세대로 넘어가게 되는 방식인데 더 젊은 세대(금방 생성)일수록 자주 GC의 프로세스에서 할당 해제할 오브젝트인지 판단이 내려지게 된다.  

이 과정을 보조적으로 추가하면서 python에서는 조금더 효율적으로 메모리를 관리 하고 있다.

<center>

<img src="https://plumbr.io/app/uploads/2015/05/object-age-based-on-GC-generation-generational-hypothesis.png" alt="Generational GC" width="500px"/>

</center>

### reference
* [Garbage Collection in Python](https://medium.com/dmsfordsm/garbage-collection-in-python-777916fd3189)
* [Garbage collection (computer science)](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science))