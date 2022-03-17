---
title: 부스트 캠프 ai tech 1주 3일차 Python Basic for AI (7)
date: 2022-01-19 08:57:34
tags:
- python
- week1
categories:
- boostcamp
- week
widgets: null
---
***
## 11. Object Oriented Programming (객체 지향적 프로그래밍, OOP)
* `객체(Object)란?`  
  프로그램에서 사용되는 데이터 또는 식별자에 의해 참조되는 공간, 독립된 단위를 의미한다
* OOP는 여러개의 독립된 객체들의 모임으로 프로그램을 구성하는것을 이야기한다

### 11.1 Object in Python
* Python에서의 객체는 class로 선언이 가능하다
* class는 속성(Attribute)와 명령어(Method)을 가지고 있다
  * Attribute  
  해당 class가 가지고 있는 특별한 변수를 말한다. 이 변수는 다른 객체가 될 수도 있다. \_\_init\_\_(self) 메서드로 속성을 미리 설계할 수 있다
  * Method  
  해당 class가 내장하고 있는 함수들을 지칭한다. 메서드는 class 안에 기존 함수와 같은 방식으로 정의가 가능하나, 반드시 self를 추가해야 메서드로 인정된다. 또한 python에는 특별한 메서드 들이 존재한다
* class의 이름 선언과 함께 \_\_init\_\_메서드에 parameter 값들을 입력하면 객체를 생성 할 수 있다
* class_name.method_name()과 같은 형식으로 객체의 메서드를 호출 할 수 있다

* 예시 축구선수

```python
class SoccerPlayer(object):
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number
        
    def change_back_number(self, new_number):
        print("선수의 등번호를 변경합니다 : From %d to %d" % (self.back_number, new_number))
        self.back_number = new_number
        
    def kick(self):
        pass
    
    def heading(self):
        pass
    
    def moving(self):
        pass

jinhyun = SoccerPlayer("Jinhyun", "MF", 10)
print("현재 선수의 등번호는 :", jinhyun.back_number)
jinhyun.change_back_number(5)
print("현재 선수의 등번호는 :", jinhyun.back_number)
==================================================
output:
현재 선수의 등번호는 : 10
선수의 등번호를 변경합니다 : From 10 to 5
현재 선수의 등번호는 : 5
```

### 11.1.1 Special method
* class에는 \_\_init\_\_ 과 같이 특정한 일을 전담하는 정해진 메서드들이 존재하고 이것들을 Special method라고 부른다
* class 내부에 Special method를 정의하면 객체간의 operator 연산 등 여러가지를 할 수 있다.
* 자세한 내용은 링크로 남기고 생략한다.
* [여러가지 스페셜 메서드](https://www.informit.com/articles/article.aspx?p=453682&seqNum=6)

### 11.2 OOP의 특징
* `Visibility` 가시성
  * `객체의 정보를 볼수 있는 레벨을 조절한다`
  * 유저에게 필요한 부분은 보여주고(`추상화`), 노출할 필요가 없는 정보들은 숨긴다(`캡슐화`)
  * \_\_ 를 속성이나 메서드 앞에 붙여서 객체 외부에서 접근할 수 없게 한다 
  * ~~결론 : docstring 잘 쓰는게 중요하다~~
* `Inheritance` 상속
  * 부모클래스로부터 속성과 Method를 물려받은 자식클래스를 생성 하는 것을 말한다
  * super를 통해 부모클래스의 메서드를 호출 할 수 있다
  * 코드의 재사용이 목적이다
* `polymorphism` 다형성
  * 같은 이름의 메서드의 내부로직을 다르게 사용할 수 있다.
  * 자식클래스에서 메서드를 재정의(overiding)하여 새로 맞춰서 사용이 가능하다

```python
class TeamAPlayer(SoccerPlayer):
    def __init__(self, regular):
        super().__init__(name, position, back_number)
        self.regular = regular
    
    def is_regular(self):
        print(self.name, '선수는 주전', '입니다' if self.regular else '이 아닙니다')
    
    def change_back_number(self, new_number):
        print(f"팀 A {self.name}선수의 등번호를 변경합니다")
        super().change_back_number()
        self.back_number = new_number

jinhyun = TeamAPlayer("Jinhyun", "MF", 10, False)
jinhyun.is_regular()
jinhyun.change_back_number(5)
=============================
output:
Jinhyun 선수는 주전 이 아닙니다
팀 A Jinhyun선수의 등번호를 변경합니다
선수의 등번호를 변경합니다 : From 10 to 5
```
***
## 참고 자료
[객체 지향 프로그래밍 - wikipedia](https://en.wikipedia.org/wiki/Object-oriented_programming)