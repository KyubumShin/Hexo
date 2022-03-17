---
title: Linux 커맨드
date: 2022-02-14 11:20:02
tags:
- DeepLearning
- week5
- Linux
categories:
- boostcamp
- week
widgets: null
mathjax: true
---
***
## Linux Command
### 기본 커멘드
* man [command]
  * 쉘 커맨드의 매뉴얼 문서를 출력해준다
* mkdir [name]
  * name의 이름을 가진 directory를 생성한다
* ls
  * 현재 접근한 폴더의 폴더, 파일 확인
  * a: 현재 접근한 폴더의 전체 파일 출력(.으로 감춰진 폴더까지 전부)
  * l: 권한, 소유자, 만든날짜, 용량까지 출력
  * h: 용량을 보기쉽게 GB, MB등으로 표현
* pwd
  * 현재 폴더의 경로를 절대경로로 표시
* echo
  * 'text': 터미널에 텍스트를 출력
  * "command": 터미널에 커멘드의 출력한 결과를 출력해준다
* sudo [command]: 슈퍼유저로 프로그램을 실행
* clear
  * 커멘트 창을 깨끗하게 해준다  
* history
  * 최근에 입력한 쉘 커맨드 History 출력
  * !number 를 통해 커맨드 재활용 가능하다
* export
  * 환경변수를 지정할 수 있다.
  * 커널을 종료하면 날아가니까 .bashrc 등에 적으면 영구적으로 사용가능하다
* alias
  * 기존 커맨드의 별칭을 지정할 수 있다
  * ex) alias ll2='ls -l'

### 파일 관리 관련 커맨드
* cp [filename] [newfilename]
  * Copy
  * -r : directory 내부의 모든 파일도 같이 복사
  * -f : 강제로 복사
* mv [filename] [newfilename]
  * 파일 옮기기(혹은 이름바꾸기)
* cat [files] (\> or \>\> [filename]) 
  * 특정 파일 내용 출력
  * 여러파일을 인자로 주면 합쳐서 출력
  * \> : 파일을 저장하고 overwrite
  * \>\> : 파일에 추가하는 경우
* head, tail [number]
  * 파일 앞/뒤의 n행 출력
* sort
  * 말 그대로 sort
* uniq
  * 중복되는 라인을 제거하는 명령어
  * c : 제거된 라인을 count한다

### 서버 관련 커맨드
* ps
  * 현재 실행되고 있는 프로세스 출력
* curl
  * 웹서버 작성 후 Request 테스트 하는 명령어
* df
  * 디스트 용량확인
  * -h로 가독성을 높임
* scp
* chmod
  * 파일의 권한을 변경하는 경우 사용한다
  * r 읽기권한 4
  * w 쓰기권한 2
  * x 실행권한 1
  * 수를 합쳐서 표기하면 여러개의 권한을 나타낼 수 있다

### reference
* [Naver Connect Boostcamp - ai tech](https://boostcamp.connect.or.kr/program_ai.html)