---
title: Docker
date: 2022-02-15 11:28:39
tags:
- DeepLearning
- week5
- Docker
- Ai serving
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Docker
* 리눅스의 응용 프로그램들을 프로세스 격리 기술을 사용하여 컨테이너로 실행하고 관리하는 오픈 소스 프로젝트이다
* 도커는 아래와 같은 주요 구성 요소들이 존재한다
  * 이미지
  * 컨테이너
  * 데몬
### Docker image
* 서비스 운영에서 필요한 프로그램, 소스코드, 각종 모듈, 컴파일된 실행파일을 묶는 형태를 말한다
* 간단히 말해서 프로세스를 실행하기 위해 필요한 모든 파일과 설정값을 저장하고 있어서 추가적으로 의존성 파일을 설치할 필요없는 상태이다
* Image는 Layer로 이루어져 있다
* image를 build할때 효율적으로 동작하기 위해 구현된 층을 Layer라고 한다
  * image는 여러개의 읽기전용 Layer로 구성되어 있다
  * 다른 image를 받아와서 그위에 Layer를 쌓아 새로운 Image를 만드는것도 가능하다
  * 아래의 명령어 한줄한줄이 Layer라고 생각해도 무방하다
```Dockerfile
FROM pytorch/pytorch:1.7.0-cuda11.0-cudnn8-runtime
RUN apt-get update -y
...
WORKDIR /app
COPY ./src /app/src
COPY ./test /app/test
ENTRYPOINT python3 /app/src/run.py
```
* 이를 통해 컨테이너를 생성할 수 있다

### Docker Container
* Image를 실행, 응용프로그램 자체를 `격리된 공간에서 동작`시키는 기술이다
* Image를 통하여 여러대의 Container를 생성 할 수 있고, `이 Container들은 모두 동일한 개발환경을 가지게 된다`
  * Docker의 장점 1
  * 여러대의 분리된 서버를 모두 같은 환경으로 만들 수 있다
* Image를 실행시키기만 하면 Image에 저장되어있던 모든 파일들과 환경변수등이 셋팅되기 때문에 설치가 매우 간편하다
  * 장점 2

### Docker Daemon
* Docker Container나 Image를 관리하는 Kernel
* user가 client를 통해서 보낸 명령을 받아서 Docker 객체들을 관리한다
* 하나의 커널로 여러 Container를 관리하기 때문에 가상환경에 비해 도커가 용량을 덜 차지하고, 더 빠른 속도를 가질 수 있다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)