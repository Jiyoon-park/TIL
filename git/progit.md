# ProGit

* 1, 2, 3, 5 먼저 볼 것
* https://git-scm.com/book/ko/v2

## 1. 시작하기

#### 버전관리란?

버전 관리 시스템은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다.

#### CVCS 중앙 집중식 버전 관리

다른 개발자와 함께 작업해야 하는 경우가 많다. 이럴 떄 생기는 문제를 해결하기 위한 중앙집중식 CVCS.

단점 ) 중앙 서버에서 다운되면 그 동안 아무도 다른 사람과 협업할 수 없고 백업할 수도 없다. 중앙 데이터베이스가 있는 하드디스크에 문제가 생기면 모든 히스토리 잃음.

#### DVCS 분산 버전 관리

저장물을 전부 복제. 서버가 망가져도 클라이언트 저장소 중에서 아무거나 하나 가져와서 복구하면 된다.



## 2. Git 의 기초

### 2-1. Git 저장소 만들기

#### 1) 기존 디렉토리를 Git 저장소로 만들기

```bash
#깃 저장소 만들기
$ git init 

#파일 추가
$ git add <filename>

#커밋
$ git commit -m "<commit ms>"
```

#### 2) 기존 저장소를 Clone 하기

```bash
$ git clone <url>
```



### 2-2. 수정하고 저장소에 저장하기

 워킹 디렉토리 안의 파일의 상태는 `untracked`, `tracked`( `unmodified`, `modified`, `staged` ) 중 하나이다.

* untracked : 스냅샷(커밋)에 넣어지지 않은 파일
* tracked : 스냅샷에 넣어진 파일

```bash
#파일 상태 확인
$ git status 
$ git status -s

#파일 변경 내용 보기
$ git diff 
$ git diff --staged 
$ git diff --cached

#staged 상태로 만들기 - 다음 커밋에 추가
$ git add <filename> 

#변경사항 커밋하기
$ git commit
$ git commit -m "<commit msg>"

#add 없이 바로 커밋하기 (staging area 생략, tracked 상태 파일 모두 커밋)
$ git commit -a -m "<commit msg>"

#파일 삭제 - staging area와 working dir에서 모두 제거
$ git rm <filename>

#파일 삭제 - staging area에서 제거/working dir에 존재
$ git rm --cached <filename>

#파일명 변경
$ git mv <old_file_name> <new_file_name>
```



### 2-3. 커밋 히스토리 조회하기

```bash
#히스토리 조회
$ git log

#최근 n개 커밋 조회
$ git log -<n>

#각 커밋의 diff 결과 조회
$ git log -p
$ git log --patch

#각 커밋의 통계 정보 조회 - 어떤 파일이 수정? 얼마나 많은 파일이 수정? 얼마나 많은 라인이 추가/삭제?
$ git log --stat

#각 커밋을 한줄로 조회
$ git log --pretty=oneline

#원하는 포맷으로 조회
$ git log --pretty=format

#브랜치를 그래프로 출력
$ git log --graph
```



### 2-4. 되돌리기

```bash
$ git commit --amend

#staged상태의 파일을 unstaged로 상태로 변경
$ git reset HEAD <filename>

#modified 되돌리기
$ git checkout -- <filename>
```



### 2-5. 리모트 저장소

> 인터넷이나 네트워크 어딘가에 올라가있는 저장소

```bash
#리모트 저장소 확인
$ git remote -v

#리모트 저장소 추가
$ git remote add <new_remote_name> <url>

#리모트 저장소 데이터 가져오기 - fetch
$ git fetch <remote>

#리모트 저장소 데이터 가져오고 로컬 브랜치와 merge - Pull
$ git pull <remote>

#리모트 저장소에 push
$ git push <remote> <branch_name>

#리모트 저장소 정보 확인
$ git remote show <remote>

#리모트 저장소 이름 바꾸기
$ git remote rename <old_remote_name> <new_remote_name>

#리모트 저장소 삭제하기
$ git remote remove <remote>
```

#### 2-6 tag, 2-7 alias 는 아직

https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80





---

따로 학습

## branch

병렬적으로 업무 가능.

```bash
#로컬 브랜치 확인
$ git branch

#리모트 브랜치까지 모두 확인
$ git branch -r

#브랜치 생성
$ git branch <branch_name>

#브랜치 이동
$ git switch <branch_name>
$ git checkout <branch_name>

#브랜치 생성과 이동
$ git switch -c <branch_name>
$ git checkout -b <branch_name>

#브랜치 삭제
$ git branch -d <branch_name>

#브랜치 이름 변경
$ git branch --move <old_branch_name> <new_branch_name>

$ git branch -v 
$ git branch --merged
$ git branch --no-merged
```

## merge

```bash
$ git merge <target_branch>
```



#### fast-forward merges

#### three-way merges



Q ) 

이전 커밋들을 모두 merge 하는지/ 아니면 하나의 커밋으로 만들어 merge 하는지