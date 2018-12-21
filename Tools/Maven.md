# build tool
- 프로젝트 생성, 테스트, 빌드, 배포 등 기본적인 작업을 위한 전용 프로그램

# Apache Maven이란?
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
- CoC (Convention over Configuration) : 명확한 '관습'으로 인해 더 편해진다
    - 개발자는 소스나 실행 파일 디렉터리 명칭을 '그냥' 보고 알 수 있다
    - 개발자들의 관습 혹은 암묵적으로 알고 있는 디렉터리나 위치 정보, 빌드 도구들도 똑같이 사용하자
    - 설정 작업이 더 간결해지고 쉬워진다
        - 관습과 다른 내용만 명시하자
    - Conventions 혹은 defaults는 거의다, 보이지 않는 super pom에 선언되어 있다

### 핵심 개념 (Key Concept)
- 혼동하지 않도록 주의 깊게 학습해야 한다

#### Plugin
- Maven은 플러그인 실행 프레임워크
    - 플러그인 메커니즘에 의해 기능이 확장됨
    - 플러그인은 다른 artifacts와 같이 저장소에서 관리된다
- 플러그인은 goal의 집합이다
    - maven은 여러가지 플러그인으로 구성되어 있으며, 각각의 플러그인은 하나 이상의 goal(명령, 작업)을 포함하고 있다
    - goal은 플러그인과 goal 명칭의 조합으로 실행할 수 있다
- Mojo : Maven plain Old Java Object
    - 'plugin'은 새로운 mojo를 설치(추가)한다는 의미
``` 
형식 :  <plugin>:<goal>
예시 :  mvn archetype:genterate 
```
- 메이븐은 여러 goal을 묶어 "lifecycle phases"로 만들고 실행한다

#### LifeCycle
- 단계의 집합(논리적인 작업 흐름)이 라이프 사이클이다
    - maven의 동작 방식은 일련의 phase에 연계된 goal을 실행하는 것
    - build phases는 사전 정의된 순서대로 실행된다
    - 모든 빌드 단계는 이전 단계가 성공적으로 실행되었을 때, 실행된다
- 빌드 단계는 goal들로 구성된다
    - Goal은 특정 작업, 최소한의 실행 단위(task)이다
    - 각 단계는 0개 이상의 goal과 연관(associate)된다
- 메이븐은 3개의 표준 라이프사이클을 제공한다
    - clean : 빌드 시 생성되었던 산출물을 지운다
    - default : 일반적인 빌드 프로세스를 위한 모델이다
    - site : 프로젝트 문서와 사이트 작성을 수행한다
    
#### Dependency
- 라이브러리 다운로드 자동화
- 선언적 관리
    - 사용되는 jar 파일들을 어디서 다운로드 받고, 어느 버전인지 명시하면 코딩을 하지 않아도 메이븐이 알아서 관리함
- 메이븐이 관리한다.
    - lib 설정 필요 없음

#### Profile
- 서로 다른 대상 환경을 위한 다른 빌드 설정
    - 다른 운영체제, 배포환경
- 동작 방식 (Avtivation)
    - `-P` 명령행 실행환경(CLI) 옵션
    - 환경 변수 (environment variable) 기반
- 메이븐은 정상 절차 이외에 프로 파일을 위한 절차 추가로 수행한다

#### POM
- Project Object Model
- 프로젝트 당 하나의 pom.xml
    - 각각의 프로젝트는 pom.xml 파일을 하나씩 가진다
    - pom은 프로젝트 자체와 의존성에 대한 설정 및 정보를 포함한다
    - maven은 pom.xml을 읽어, 프로젝트를 가공하는 방법을 이해한다
- 3가지 `coorfinates`를 이용해 자원을 식별한다
    - group ID
    - Artifact ID
    - version
    
##### POM - 중요한 속성들
|| 속성 || 설명 ||
| artifactId | 아티펙트의 명칭, groupId 범위 내에서 유일해야 한다 |
| groupId | 프로젝트의 패키지 명칭 |
| version | artifact 현재 버전 |
| name | 어플리케이션의 명칭 |
| packaging | artifac 패키징 유형
 - POM, jar, WAR, EAR, EJB, bundle (중 선택 가능)|
| distributionManagement | artifact가 배포될 저장소 정보와 설정 |
| parent | 프로젝트의 계층 정보 |
| scm | 소스 코드 관리 시스템 정보 | 
| dependencyManagement | 의존성 처리에 대한 기본 설정 영역 |
| dependencies | 의존성 정의 및 설정 영역 | 

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
- [SlideShare 메이븐 기본 이해](https://www.slideshare.net/sunnykwak90/ss-43767933)
- [SLIPP - 자바 세상의 빌드를 이끄는 메이븐](https://www.slipp.net/wiki/pages/viewpage.action?pageId=10420233)
- [DevKuma Maven](http://www.devkuma.com/books/pages/102)