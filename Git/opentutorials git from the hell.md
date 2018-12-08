* 이 글은 egoing님의 [생활코딩 지옥에서 온 GIT](https://opentutorials.org/course/2708)강의를 학습하며 정리한 내용입니다

# 버전관리의 본질

## 저장소 만들기
```
git init
```
- 현재 디렉토리에서 작업을 시작하겠다는 것을 git에게 알려주는 명령어
- 실행하면 버전관리에 사용되는 정보들이 `.git`파일에서 관리됨

## git이 관리할 대상으로 파일 등록
```
git add file.txt
```
- `Untracked files` 중 `git`을 이용해서 관리하고 싶은 파일을 관리하도록 등록하는 명령어
	- `git status`명령으로 `Untracked files` 확인 가능
- `modified`된 파일을 현재 버전에 등록할 경우에도 사용
- 최초로 추적할 때, 변경된 파일을 버전에 등록할 때도 사용
- 선택적으로 파일을 버전에 포함시키기 위해서 사용함

## 버전 만들기 (commit)
### 버전
- 의미있는 변화
- 작업의 단위가 완결된 상태
	- 좋은 단위가 무엇인지는 고민해 볼 것

### git user 설정
```
git config --global user.name kimsunoh
git config --global user.email rlatjsdh7902@gmail.com
```
- 사용자의 이름과 이메일 정보를 설정하는 명령어
- 설정은 `~/.gitconfig`에 저장됨

### 버전 message
- `git commit`명령어를 이용해 현재 버전의 commit정보를 열고 상단에 message를 작성함
- `git log`명령어를 이용해 현재 저장소의 히스토리를 확인할 수 있음

## Stage area
- 커밋 대기 상태의 파일들이 가는 곳
- `git add`를 한 파일이 속하게 됨

### git의 공간 - Stage - repository
- Stage : 커밋 대기 상태의 파일들이 가는 곳
- repository : 커밋이 된 결과가 저장되는 곳
- working copy

## 변경사항 확인하기 - 버전관리 시스템의 효용
- 모든 버전 간의 차이점을 출력할 때
```
git log -p
```

- 버전 간의 차이점을 비교할 때
```
git diff version_id1..version_id2
```

- git add하기 전과 add한 후의 파일 내용을 비교할 때
```
git diff
```

## 과거의 버전으로 돌아가기 (reset vs revert)
```
git reset --hard version_id
```
- 현재의 로그를 취소해서 이전 버전으로 돌아가는 방법
	- hard이외의 옵션도 있음
	- 이후 git의 원리를 파악하고 난 이후 나머지를 사용
- `commit`을 삭제하게 됨
```
git revert version_id
```
- 버전 id의 커밋을 취소한 내용을 새로운 버전으로 만드는 명령
- 둘의 차이를 알기 위한 참고 만화 [\[개발바보들\] Git "Back to the Future"](https://www.popit.kr/개발바보들-git-back-to-the-future/)



# git의 원리
- 원리를 파악하기 위해서는 `.git`디렉토리 하위의 git 정보가 변하는 것을 파악해야 한다

## gistory 설치
- [gitstory](https://github.com/egoing/gistory) : git을 분석하기 위한 도구

## git add의 원리
- `Git`은 `SHA1`이라는 hash알고리즘을 이용해서 `.git/objects`하위에 파일내용을 저장할 `디렉토리/파일`을 만들고 해당 파일의 내용을 저장한다
    - `디렉토리/파일`은 sha1-hash를 통해 구해진 hashid를 이용해서 만든다
- 파일의 이름은 `index`에 담겨져있고, 변경된 파일의 내용은 `objects/hashid`에 담겨져 있다
- git은 파일을 저장할 때, 파일의 이름이 달라도 파일의 내용이 같으면 같은 `object`파일을 가르킨다
    - 반복적인 내용을 갖고 있는 파일들의 저장공간을 효율적으로 관리할 수 있다
      
## objects 파일명의 원리
- 내용을 기반으로 파일의 이름을 결정하는 매커니즘의 이해
- 파일내용으로 sha1(hash알고리즘)으로 hashkey를 생성해서 앞 두글자로 디렉토리를 만들고, 뒷부분을 이름을 가진 파일에 내용이 저장이된다
    - 파일의 내용과 다른 정보들도 포함되어 hashkey를 만들것이다

### objects 파일의 종류 3가지
- blob : 파일의 내용을 담고 있음
- tree : 어떤 디렉토리의 명과 blob의 정보를 담고 있음
- commit : 커밋의 정보를 담고있음

## commit의 원리
- `commit` 버전은 `objects 파일`로 저장이되고, 그 파일의 내부에는 버전에 대한 정보가 ```tree objects파일명```의 형태로 저장이 되어있다.
- `commit` 버전의 `objects 파일`의 내부에는 `parent objects파일명`이 있다
    - 이것은 지금 `commit` 버전의 전 `commit` 버전의 정보이다
- 각각의 버전은 각각의 버전이 만들어진 시점의 스냅샷을 저장해놓는다. 통해서 그 파일의 정보를 파악할 수 있다.  
- `commit` 에는 두가지 중요한 정보가 담겨져 있다

### commit의 두가지 정보
- parent 값
    - 이전 `commit` 버전의 정보를 탐색 할 수 있음
- commit이 일어난 시점의 작업디렉토리에 있는 파일의 이름과, 이름이 담고있는 내용의 관계정보가 담겨져있다
    - 버전이 만들어진 시점의 프로젝트 폴더에 대한 상태를 알 수 있다.
    
## status의 원리(추정)
- `.git` 하위의 `index`와 최신 commit objects의 `tree`의 내용이 같다면 현재 commit 할 것이 없다는 것
- 파일이 수정되었다는 것을 알려주는 방식은 현재파일 내용의 sha1-hash값과 `index`의 파일 `hashid`가 다르다면 파일의 내용이 수정되었다는 것을 알 수 있음
- 'git add'된 파일과 수정된 파일의 차이는 `add`를 하게 되면 `index`의 파일A `hashid`와 파일A의 현재파일의 sha1-hash값이 같다면 파일이 `add` 되었다는 것을 알 수 있다. 그리고, `Git`은 `index`의 내용과 최신 `commit tree`의 `objects`가 가르키는 내용과 다르다면 현재 파일A의 내용은 `index`에 `add`되어서 `commit` 대기상태임을 알 수 있다
- `index`와 `commit tree` 사이의 관계
    - `workspace`-`index(staging area, cache)`-`reepository` 사이의 관계를 이해해라
