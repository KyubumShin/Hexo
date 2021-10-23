---
title: critical_data_structure
date: 2021-10-15 13:26:05
tags:
categories:
---
# critical Data Structures
## 간략한 요약 
* sk_buff  
패킷이 저장되는곳  
이 구조는 모든 네트워크 레이어에서 그들의 header와 유저데이터에 관한 정보(payload), 내부적으로 협력하기위해(다른 레이어들과)필요한 다른 정보들이 있는지를 저장하는데 사용함 

* net divice  
각각의 network device는 하드웨어와 소프트웨어 설정을 가진 데이터 구조로 커널안에서 나타내어진다.  
8챕터에 어떻게 할당할지 자세하게 나옴

## The Socket Buffer: sk_buff Structure
네트워킹 코드에서 가장 중요한 데이터 구조 -> 왜?
받는것과 보내는것에 대한 헤더를 나타내기 때문에

sk_buff는 L2 (MAC, 프로토콜 같은 물리계층), L3(IP), L4(TCP, UDP) 에서 사용됨
다른레이어 전달될때마다 필드의 구조가 적절히 바뀐다.  
L4 -> L3같이 낮은 계층으로 전달될때는 구조체에 header가 appending된다. -> 복사하는것보다 효율적 : 구조체공간 추가하는 함수는  skb_reseve인데 이따 설명한다.  
L3 -> L4 같이 높은 계층으로 전달될때는 header의 포인터값만 해당 레이어의 header위치로 바뀐다. (삭제하지 않음)

## Networking Options and Kernel Structures


The Socket Buffer는 4가지 카테고리로 나타내어짐
Layout
General
Feature-specific
Management functions

## Layout Fields
sk_buff는 조금 복잡한 doubly linked list 로 이루어져 있음
그래서 next, prev를 가르키는 포인터로 묶여있는 구조를 가진다.
이 리스트들은 head를 빨리 찾아야하는 필요가 있음 -> 그래서 리스트 맨 처음에 dummy list가 아닌 sk_buff_head가 들어감  

sk_buff_head 구조
```C
struct sk_buff_head {
    /* These two members must be first. */
    struct sk_buff * next;
    struct sk_buff * prev;
    _ _u32 qlen;
    spinlock_t lock;
};
```
* qlen : 리스트의 elements 수
* lock : 리스트에 동시접속을 막기위해 사용(아래에서 설명함)

그리고 또한 sk_buff에서도 head를 빠르게 찾기위해 sk_buff_head를 가르키는 포인터(list)가 구조에 포함되어있음

```C
struct sk_buff {
    /* These two members must be first. */
    struct sk_buff * next;
    struct sk_buff * prev;
    struct sk_buff_head *list;
    ...
};
```
그 외 fields
``` c
struct sock *sk
```
* struct sock *sk  
  * 이 버퍼를 소유한 socker에 대한 포인터. 
  * 로컬에서 데이터가 생성되었거나, 로컬프로세스가 데이터를 받고있는 상황에 L4나 유저 app에서 소켓에 대한 정보를 필요로 하기때문에 사용한다.
* unsigned int len  
  * 버퍼 안에 있는 데이터 블록의 크기(main buffer + fragments의 데이터를 합친 크기, fragments는 21챕터에서 다룰 예정)이다. 
  * headers가 레이어사이를 이동할때마다 더해지거나 버려지기 때문에 레이어 사이를 움직일때마다 크기가 변한다.
* unsigned int data_len
  * fragments의 데이터 사이즈만 포함하고 있다
* unsigned int mac_len
  * MAC header의 크기
* unsigned int truesize
  * buffer의 총 사이즈
  * len + sizeof(sk_buff)로 초기화
  * len이 바뀔때 업데이트됨
* atomic_t users
  * sk_buff를 이용하는 엔티티의 수
  * 실제로 사용중인 sk_buff의 락을 해제하는일을 회피하기위해 주로 사용됨
  * user는 필요할때 이 수치를 조절가능, 뒤 챕터에서 자세하게 다룰 예정
* unsigned char *head, *end, *data, *tail
  * buffer와 data의 경계선
  * header나 data가 추가될 상황을 고려하여 미리 만들어둔 공간의 경계를 나타낸다.
  * 아래 그림 추가요망

![]()그림들어갈곳

* void (*destructor)(...)
  * 버퍼가 삭제될 때 실행되는 루틴
  * 버퍼가 소켓에 할당되어있지 않을때 보통 초기화 되지않음
  * 버퍼가 소켓에 할당되면 sock_rfree나 sock_wfree 로 설정됨

## General Fields
특정 커널의 기능들과 연관되지않은 대부분의 sk_buff fields를 다룬다.
* struct timeval stamp
  * 수신되었거나 가끔 전송이 예약된 패킷을 나타내는 timestamp를 말한다.
  * netif_rx, net_timestamp에 의해 설정되는데 21챕터에서 다룰예정
* struct net_device *dev
  * dev 패킷을 저장하고 있는 상황에선 어떤 네트워크 장치로부터 패킷을 받았는지를 나타내고, 패킷을 보내는 상황에선 패킷을 내보낼 장치를 나타낸다.
  * 뒤에 자세히 다룰 예정
* struct net_device *input_dev
  * 패킷을 받은 디바이스를 나타낸다.
  * 패킷이 로컬에서 생성되었으면 NULL pointer를 가르킴
* struct net_device *real_dev
  * 가상 장치일때 가상장치와 연관된 실제 device를 가르킴
  * The Bonding and VLAN interfaces 등에서 사용
* union {...} h, nh, mac
  * TCP/IP 스택의 protocol header를 가르키는 포인터
  * h : L4
  * nh : L3
  * mac : L2
  * 레이어간 이동을 할때 skb->data에서 이 포인터들을 참조하여 자신의 header의 포인터를 변경한다.
* 