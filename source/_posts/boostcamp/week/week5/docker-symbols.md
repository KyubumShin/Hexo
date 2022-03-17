---
title: 윈도우, Linux 그리고 Docker
date: 2022-02-18 13:45:49
tags:
- DeepLearning
- week5
- Docker
- Linux
- Ai serving
categories:
- Programming
- Docker
---
***
부스트 캠프를 진행하던 도중 질문게시판에 mlflow를 윈도우에서 돌렸는데 에러가 발생했다고 올라와서 궁금해서 조사하던 도중 알게된 사실과 추가적으로 궁금해서 찾아본 것들에 대해 정리해 보고자 한다

<center>

<img src="/img/error.png" alt="" width="600px"/>

</center>

### 발생한 문제점
* `docker: Error response from daemon: invaild mode: 경로`와 같은 에러가 발생하였다.

### 조사과정
* 평소 python에서 코딩을 할 경우에도 /와 \\를 혼용해서 사용하면 매우 쉽게 에러가 발생하는 모습을 보았기 때문에 Linux기반인 docker에서 windows 명령어를 사용해서 에러가 나는것이 아닐까 생각하였다

### 알게된 점
* 원인은 : symbol에 존재했다. 윈도우에서는 : symbol을 C:\\directory식으로 드라이브를 표기할 때 사용하지만, mount할때에는 : 를 연동할 대상의 구분자로 사용을 하기 때문이다
* docker 에서 volumn mount를 시행할 시 입력되는 경로는 무조건 절대경로로 적어야한다. pwd로 입력해야한다고 doc에 나와있었다

### 해결 방법
* C: 형태를 //C/directory 형태로 바꿔서 입력을 한다
  * 기존 윈도우에서 사용하는 형태를 리눅스 커맨드 형태로 바꿔서 입력한다
  * 어차피 docker 내부에서 작동할 커맨드이기 때문에 윈도우 커널에서도 잘 돌아간다
* ""로 한번 감싸준다
  * ""로 싸주어서 전체 C:\\가 링크인것을 알려준다


### 결론
* 기본적으로 docker는 Linux 기반이기 때문에 windows로 사용할 경우 많은 제약이 당연하게도 뒤따른다
* windows에서 Docker를 쓸 때는 WSL을 이용하자

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)
* [docker toolbox Docker Volume, Error response from daemon: invalid mode](https://m.blog.naver.com/dbwodlf3/221823831023)