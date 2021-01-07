# ProGit

* https://git-scm.com/book/ko/v2

## 1. 시작하기

#### 버전관리란?

버전 관리 시스템은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다.

#### CVCS 중앙 집중식 버전 관리

다른 개발자와 함께 작업해야 하는 경우가 많다. 이럴 떄 생기는 문제를 해결하기 위한 중앙집중식 CVCS.

단점 ) 중앙 서버에서 다운되면 그 동안 아무도 다른 사람과 협업할 수 없고 백업할 수도 없다. 중앙 데이터베이스가 있는 하드디스크에 문제가 생기면 모든 히스토리 잃음.

#### DVCS 분산 버전 관리

저장물을 전부 복제. 서버가 망가져도 클라이언트 저장소 중에서 아무거나 하나 가져와서 복구하면 된다.



#### git workflow

* working dir -- (add) -- staging area -- (commit) -- .git fir -- (push) -- remote repo



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

#각 커밋의 diff 결과 조회 (자세히 알고싶어!)
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

#로그 원라인으로 그래프로 출력
$ git log --oneline --graph

#로그 원라인으로, 브랜치가 가리키는 커밋 확인
$ git log --oneline --decorate

#bree가 커밋한 것만
$ git log --author="bree"

#2020-12-01 이전의 커밋만
$ git log --before="2020-12-01"

#원하는 string이 커밋 타이틀에 들어간 것만
$ git log --grep="{target_str}"

#원하는 string이 소스코드 컨텐츠 안에 들어간 것만
$ git log -S "{target_str}"

#원하는 파일의 커밋만 보고 싶어
$ git log <file_name>
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

#### 2-6 tag

> 특정 커밋을 북마크해두고 싶을 때. 보통 릴리즈 버전을 이용할 때 사용한다.

* v2.0.0

  * major

    커다란 기능 추가, 전체적 업데이트

  * minor

    커다란 기능 중 조금의 기능들 업데이트

  * fix

    기존 기능의 오류 수정, 성능의 개선

```bash
#태그를 남기고 싶다면?
$ git tag v2.0.0 <commit_code>

#조금 더 자세한 태그를 남기고 싶다면?
$ git tag v1.0.0 <commit_code> -am "{msg_info}"

#태그 다 조회
$ git tag

#특정 버전이 포함된 태그만 보고 싶어
$ git tag -l "v1.0.*"

#특정 태그 삭제
$ git tag -d v.1.0

#원하는 태그로 이동
$ git checkout v2.0.0
```



#### 2-7 alias 는 아직

https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80



#### +) 추가적으로 알아둘 것

```bash
#현재 head의 이전 부모로 이동
$ git checkout head~1

#현재 head의 이전이전 부모로 이동
$ git checkout head~2

#현재 head의 이전이전이전 부모로 이동
$ git checkout head~3

#오래된 커밋부터 보기
$ git log --oneline --reverse

#원하는 정보를 예쁘게 포맷
$ git log --pretty=oneline
$ git log --pretty=format:"%h %an %ar %s"
$ git log --oneline --graph --all

#git hist 설정하기
$ git config --global alias.hist "log --graph --all --pretty=format:'%C(yellow)[%ad]%C(reset) %C(green)[%h]%C(reset) | %C(white)%s %C(bold red){{%an}}%C(reset) %C(blue)%d%C(reset)' --date=short"
```





## Git 브랜치

### 3-1. 브랜치란 무엇인가

> 코드를 통째로 복사하고 원래 코드와 상관없이 독립적으로 개발 진행이 가능하게 하는 것이다. 덕분에 병렬적으로 개발이 가능하다.

* HEAD : 현재 작업 중인 브랜치

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

#브랜치 + 각 브랜치의 마지막 커밋
$ git branch -v 

#현재 브랜치 기준으로 이미 merge된 브랜치 확인 - '*' 붙은 브랜치 제외하고 삭제해도 됨.
$ git branch --merged

#현재 브랜치 기준으로 아직 merge 안 된 브랜치 확인
$ git branch --no-merged

#특정 브랜치 기준으로 merge 안 된 브랜치 확안
$ git branch --no-merged <target_branch>
```



### 3-2. 브랜치와 merge의 기초

* fast-forward merges 

  > master가 target_branch의 조상인 경우, fast-forward merge가 가능하다.  작업이 끝나면 마스터로 checkout 한 후, 타겟 브랜치를 merge 하면 된다. 결과적으로, master 브랜치가 최신 커밋으로 이동하고 최신 커밋을 브랜치가 가르키게 된다. 이 방법은 히스토리에 머지되었다는 사실이 남지 않는다.(깔끔한 것은 장점이지만, 히스토리가 남지 않는다는 것은 단점일수도.) 

```bash
$ git checkout master
$ git merge <target_branch>

#fast-forward commit 남기기
$ git merge --no-ff feature-c
```

* three-way merges

  >각 브랜치가 가리키는 커밋 두개와 공통 조상 하나를 사용해 커밋 3개를 머지하는 방법을 three-way merge라 한다. 단순 브랜치 포인터의 이동이 아니라, 3-way merge를 진행한 결과를 별도의 커밋으로 만들고 그 결과를 브랜치가 가리키도록 한다.

* conflict

  > merge 하는 두 브랜치가 같은 파일의 같은 부분을 수정했을 때 일어난다. Git이 어떤 코드를 살려야할 지 모르기에, 개발자가 충돌을 해결하고 merge를 진행해야 한다.

  ```bash
  #1.충돌이 난 파일을 살펴보고
  $ git status
  
  #2.충돌을 해결한다.
  
  #3.해결한 파일을 git에 저장한다.
  $ git add <file_name>
  ```



### 3-5 / 3-6 다시 봐야돼. 아직 이해 못했잖아.

### 3-5. 리모트 브랜치 

```bash
#리모트 레포의 모든 리모트 브랜치와 정보 조회
$ git remote show <remote_repo_name>
```

> * remote branch
>
> * remote tracking branch
>
>   리모트 브랜치를 추적하는 레퍼런스이자 브랜치이다. 일종의 북마크이며 로컬에서 임의로 움직일 수 없다. 리모트 서버에 연결할 때마다 리모트 브랜치 업데이트 내용에 따라 자동 갱신된다. 

```bash
#로컬 브랜치 리모트 저장소로 전송
$ git push <remote_repo_name> <local_branch>

#로컬에 리모트 브랜치 정보 업데이트
$ git fetch <remote_repo_name>

#로컬에 리모트 브랜치 정보를 머지하려면
$ git merge <remote_branch>

#fetch + merge
$ git pull <remote_branch>
```



### 3-6. Rebase하기

* 서로 다른 브랜치를 하나로 합치는 것으로 merge와 목적은 같지만 rebase는 깔끔한 선형 히스토리를 만들 수 있다. 보통 리모트 브랜치에서 커밋을 깔끔하게 적용하고 싶을 때 사용한다.

* 다른 개발자와 함께 같은 브랜치에서 작업 중이라면 하지 말아야 한다. 서버에 업데이트 되지 않은 나의 로컬에 한해서 해야한다. 
* 브랜치에서 나 혼자 작업하거나 로컬에서 작업할 때 굉장히 유용

```bash
$ git rebase master

$ git rebase --onto
```





Q ) 

이전 커밋들을 모두 merge 하는지/ 아니면 하나의 커밋으로 만들어 merge 하는지