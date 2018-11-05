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

## 명령의 빈도와 메뉴얼 보는 법


