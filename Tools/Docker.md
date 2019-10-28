# Docker
- *격리*된 환경을 만들어주는 도구
    - 컨테이너 안에서 가상공간을 만들지만, 실행파일을 호스트에서 직접 실행
    - 이 기능을 리눅스와 커널의 cgroups와 namespaces가 제공함
- 어플리케이션 컨테이너를 만들어 주는 걸 목표로 함

## 가상 머신의 문제점
- 이미지 안에 OS가 포함되기 때문에 이미지 용량이 커짐
    - 네트워크로 가상화 이미지를 주고 받는게 부담됨
- 오픈소스 가상화 소프트웨어는 OS 가상화에만 주력
    - 배포와 관리 기능 부족
- 결국, 가상 머신의 문제점을 보완하기 위해 리눅스 컨테이너가 나옴

## Docker 특징
- 게스트 OS를 설치하지 않음
    - 이미지에 서버 운영을 위한 프로그램과 라이브러리만 격리해서 설치
    - 이미지 용량이 줄어듬
- 도커는 하드웨어 가상화 계층이 없음
    - 메모리 접근, 파일시스템 등 실행 환경의 자원을 사용하는 속도가 가상 머신에 비해 월등히 빠름
- 이미지 생성과 배포에 특화됨
    - 이미지 버전 관리 기능과 중앙 저장소 제공 
        - Docker Hub 제공    

## image? container?
- image
    - 서비스 운영에 필요한 서버 프로그램, 소스 코드, 컴파일된 실행 파일을 묶은 형태
    - 저장소에 올리고 받는건 이미지
    - 실행파일, 라이브러리, 소스 등을 묶은 이미지 파일
- container
    - 이미지를 실행한 상태
    - image로 여러개의 container를 만들 수 있음
- e.g. image는 실행파일, container는 프로세스  

### Docker의 image 관리
- 베이스 이미지에서 바뀐 부분만 이미지로 생성
    - 유니온 파일 시스템 형식을 사용
- Docker Hub 및 개인 저장소에서 이미지를 공유할 때 *바뀐 부분만 주고 받음*
- 각 이미지는 의존관계가 형성
- 컨테이너로 실행할 때는 베이스 이미지와 바뀐 부분을 합쳐서 실행

# Docker 기본 사용법
- 설치는 [dockerhub - Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)에서 Doker.dmg 다운 후 진행

## container 실행하기
- 명령어
```
$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

// ubuntu 16.04 container
$ docker run ubuntu:16.04
```
    - run 
- 자주 사용되는 옵션
| 옵션 | 설명 | 
| --- | --- |
| -d | detached mode (백그라운드 모드) |
| -p | 호스트와 컨테이너의 포트 포워딩 |
| -v | 호스트와 컨테이너 디렉토리 마운트 |
| -e | 컨테이너 내에서 사용할 환경변수 설정 |
| -name | 컨테이너 이름 설정 |
| -rm | 프로세스 종료시 컨테이너 자동 제거 |
| -it | -i 와 -t를 동시에 사용한 것, 터미널 입력을 위한 옵션 |
| -link | 컨테이너 연결 [컨테이너:별칭] |


## 명령어
```
// 이미지 검색
$ docker search ubuntu

// 이미지 받기
$ docker pull ubuntu:latest

// 이미지 목록 출력하기
$ docker images

// 컨테이너 실행하기
$ docker run -i -t --name hello ubuntu /bin/bash

// 컨테이너 실행 목록 확인하기
$ docker ps -a

// 컨테이너 시작하기
$ docker container start {docker-container-name}

// 컨테이너 재시작하기
$ docker container restart {docker-container-name}

// 컨테이너에 접속하기
$ docker container attach {docker-container-name}

// 컨테이너 정지하기
$ docker container stop {docker-container-name}

// 컨테이너 삭제하기
$ docker container rm {docker-container-name}

// 이미지 삭제하기
$ docker image rm {docker-container-name}

// 모든 컨테이너 삭제하기
$ docker rm `docker ps -aq`
```

## Dockerfile
- file 내용 정보
| 키워드 | 내용 |
| --- | --- |
| FROM | 어떤 이미지를 기반으로 할지 설정 |
| MAINTAINER | 이미지 작성자 정보 |
| RUN | 이미지에서 스크립트나 명령 실행 | 
| CMD | 컨테이너가 시작되었을 때 스크립트나 명령 실행 | 
| ENTRYPOINT | 컨테이너가 시작되었을 때 스크립트나 명령 실행 \n
(docker run 에서 처리방식이 CMD와 다름) | 
| EXPOSE | 호스트와 연결할 포트 번호 설정 | 
| ENV | 환경 변수 설정 | 
| ADD, COPY | 이미지에 파일 추가 | 
| VOLUME | 데이터를 호스트에 저장하도록 설정 | 
| USER | 명령을 실행할 사용자 계정 설정 | 
| WORKDIR | 명령을 실행할 디렉터리 설정 | 
| ONBUILD | FROM으로 이미지가 사용될 때 실행할 명령 설정 | 

## 이미지 컨테이너 생성 명령
```
// 이미지 생성하기
$ docker build --tag {docker-container-name}:0.1

// 컨테이너 생성하기
$ docker run --name hello-nginx -d -p 80:80 -v /root/data:/data {docker-container-name}:0.1
```

## 기타 명령어
```
// 이미지 히스토리 살펴보기
$ docker history {docker-container-name}:0.1

// 컨테이너의 변경 사항을 이미지로 저장하기
$ docker commit -a "Foo Bar <foo@bar.com>" -m "add hello.txt" hello-nginx {docker-container-name}:0.2

// 컨테이너에서 변경된 파일 확인하기
$ docker diff hello-nginx

// 이미지와 컨테이너의 세부정보 확인하기
$ docker inspect hello-nginx
```

---
## 참고문헌
- [docker - Get started](https://docs.docker.com/get-started/)
- [초보를 위한 도커 안내서 - 도커란 무엇인가?](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)
- [초보를 위한 도커 안내서 - 설치하고 컨테이너 실행하기](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html)
- [초보를 위한 도커 안내서 - 이미지 만들고 배포하기](https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html)
- [Docker-HOWTO](http://pyrasis.com/Docker/Docker-HOWTO)
