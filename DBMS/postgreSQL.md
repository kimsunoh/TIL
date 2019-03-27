# PostgreSQL
- ORDBMS : 객체-관계형 데이터베이스 관리 시스템 
- BSD 허가권으로 배포됨
- 발음
	- 포스트그레스큐엘

## 특장점
- 유연한 객체 생성
	- SQL 차원에서 제공되는 데이터베이스 객체를 사용자가 임의로 만드는 기능이 있음
	- 연산자, 복합 자료형, 집계함수, 자료형 변환자, 확장 기능 등
- 상속
	- 테이블간 상속 관계를 지정 가능하다
	- 테이블에 저장된 자료는 상위 테이블을 조회하면, 하위 테이블에 포함된 자료도 조회 가능하다
	- 객체의 상속 개념과 동일하게, 상위 테이블의 컬럼을 그대로 상속 받으면서, 하위 테이블에만 속하는 칼럼을 추가로 만들 수 있다
- 함수
	- 저장 프로시저를 서버환경에서 사용가능하다
		- 제어문, 반복문은 사용 불가
	- 다른 언어와 결함 시킬 수 있다
		- 트리거에서 특정 언어를 사용 가능하다

# Local install
```bash
brew install postgresql@9.5
 
postgres -V
> postgres (PostgreSQL) 11.1
 
// setting for 9.5.15
// you need to have postgresql@9.5 
echo 'export PATH="/usr/local/opt/postgresql@9.5/bin:$PATH"' >> ~/.zshrc
 
// compilers to find postgresql@9.5 
export LDFLAGS="-L/usr/local/opt/postgresql@9.5/lib"
export CPPFLAGS="-I/usr/local/opt/postgresql@9.5/include"
 
// pkg-config to find postgresql@9.5
PKG_CONFIG_PATH="/usr/local/opt/postgresql@9.5/lib/pkgconfig"
 
// postgresql run cmd alias add
echo 'alias pg-start="launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist"' >> ~/.zshrc
echo 'alias pg-stop="launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist"' >> ~/.zshrc
brew services stop postgresql

// run to postgres
brew services start postgresql

// DATABASE 생성 (cmd)
createdb postgretest
// DATABASE 생성
dbname=# CREATE USER postgretest WITH PASSWORD 'teset';
CREATE ROLE

// postgres 접속
psql postgretest

// User create and grant add
postgretest=# GRANT ALL PRIVILEGES ON DATABASE postgrestest to testuser;
CREATE ROLE

// user로 접속
psql postgrestest -u testuser -W 
```
---
## 참고링크
- [PostgreSQL](https://ko.wikipedia.org/wiki/PostgreSQL)
- [한눈에 살펴보는 PostgreSQL](http://d2.naver.com/helloworld/227936)
- [getting started with postgresql on mac osx](https://www.codementor.io/engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb)
- [lesstif - PostgreSQL 설치](https://www.lesstif.com/pages/viewpage.action?pageId=31850584)