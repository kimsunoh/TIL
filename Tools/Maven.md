# Maven 준비

## build tool
- 프로젝트 생성, 테스트, 빌드, 배포 등 기본적인 작업을 위한 전용 프로그램

## Apache Maven이란?
- 오픈 소스 빌드 도구
- "중앙저장소"를 사용한 JAVA 라이브러리, 프로그램들을 관리한다

## Maven 설치 
```
wget http://mirror.navercorp.com/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
yum install apache-maven 

//	/etc/profile에 환경변수 추가 필요
MAVEN_HOME=/opt/maven  
```

## Maven 기본

### Life Cycle

#### basic
- Compile : 소스코드를 컴파일
- test : 단위 테스트 실행
- package : 컴파일된 클래스 파일과 리소스 파일들을 war혹은 jar와 같은 파일로 패키징
- install : 패키징한 파일을 로컬 저장소에 배포 (USER_HOME/.m2./)
- deploy : 패키지나 파일을 원격 저장소에 배포

#### clean
- clean : 메이븐 빌드를 통하여 생성된 모든 파일을 삭제

#### site
: 메이븐 설정파일 정보를 활용하여 프로젝트에 대한 문서 사이트를 생성
- site-deploy : 생성한 문서 사이트를 설정되어 있는 서버에 배포

# Maven quick guide
- 단계
    1. 프로젝트 생성
    2. 확인
        - 프로젝트의 루트 디렉토리 my-app과 mvn 자원이 작성되어 있는지 확인
    3.응용 프로그램의 jar 작성 및 실행
    
---
## 참고링크
- [DevKuma Maven](http://www.devkuma.com/books/pages/102)
- [SLIPP - 자바 세상의 빌드를 이끄는 메이븐](https://www.slipp.net/wiki/pages/viewpage.action?pageId=10420233)
