---
title: rabbitmq
date: 2021-09-22 18:00:59
tags: 
- backend
- message
categories:
- 백엔드
- 메세지큐
---
KDT과정에서 만든 프로젝트의 실사용자가 여럿인 경우를 가정하고(그럴일은 거의 없겠지만) 백엔드를 구성하려고 팀원들과 계획을 해서 Rabbitmq를 사용하기로 결정하여 공부했었던 내용을 정리해 보았다.

RabbitMQ는 오픈소스 메세지 브로커로써 메세지를 많은사람들에게 전달하거나, request에 대한 처리시간이 길 때 등 비동기적인 처리를 할 때 사용된다.

# Model

RabbitMQ는 아래와 같이 AMQP(Advanced Message Queuing Protocol)에 따른 구조로 되어있다.


![image](https://www.rabbitmq.com/img/tutorials/python-three-overall.png)


##  **Producer(P)**
* 메세지를 생성하고 Queue에 보내 저장하는 주체이다.
##  **Consumer(C)**
* 메세지를 수신하는 주체이다.
## **Exchange(X)**
* Producer로 부터 수신한 메세지를 각각의 키에 따른 규칙(Binding)으로 Queue나 다른 Exchange로 보내주는 라우터의 기능을 가지고 있다. 
* 모든 Queue는 반드시 Exchange를 통해 메세지를 Producer로 부터 전달받는다.
## **Queue(Red Box)**
* 자료구조에서 흔히 들어왔던 큐이다. 메모리에 메세지를 저장하고 Consumer로부터 큐에 요청이 들어오면 저장되었던 메세지를 Consumer에게 전달한다.

# Exchange Type
producer로부터 생성된 모든 메세지들은 반드시 Exchange에서 Exchange Type과 Binding 규칙에 따라 규칙에 알맞은 Queue로 전달된다. Exchange Type은 다음과 같은 속성을 가진다.
* Direct Exchange
  * 메세지에 포함된 routing Key를 기반으로 **동일한** binding key를 가진 Queue에 연결된다.

![image](https://www.rabbitmq.com/img/tutorials/direct-exchange.png)
* Fanout Exchange
  * Exchange에 연결된 모든 Queue에 동일한 메세지를 전달한다.
* Topic Exchange
  * routing Key와 binding Key가 **부분적**으로 일치하는 모든 Queue 로 메세지를 전달한다.
  * 닷( . )으로 구분된 binding key를 사용하며 ```*```와 ```#```을 이용하여 binding Key를 구성할 수 있다. ```*```은 한개의 단어를 나타내고 ```#```은 0개 또는 1개의 단어를 나타낸다.

![image](https://www.rabbitmq.com/img/tutorials/python-five.png)

* Header Exchange
  * key-value 로 정의된 헤더에 의해서 전달할 Queue를 결정한다. 
  * Queue를 바인딩 할 때 x-match라는 argument로 헤더를 하나만 충족켜도 되는지(any : OR의 기능), 모든 헤더를 충족시켜야 하는지(all : AND의 기능) 규칙을 정할 수 있다.


# reference
* [AMQP Introduction](http://egloos.zum.com/killins/v/3025514)  
* [RabbitMQ Tutorials](https://www.rabbitmq.com/getstarted.html)
* [RabbitMQ란? by Eric](https://blog.dudaji.com/general/2020/05/25/rabbitmq.html)
