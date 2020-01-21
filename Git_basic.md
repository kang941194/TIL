# Git Basic

> Git은 분산형 버전 관리 시스템이다.
>
> 소스코드의 이력을 확인하고, 협업 단계에서 활용할 수 있다.



## 1. 기본 설정

* 윈도우에서 Git을 활용하기 위해서는 `git bash`가 필요하다.

  * [Git for Windows](https://gitforwindows.org/)

* 기본적으로 소스코드의 버전 정보를 기록하는 작성자(`author`) 설정이 필요하다.

  ```bash
  $ git config --global user.name "kang941194"
  $ git config --global user.email "kang941194@nate.com"
  ```

* 설정한 작성자 정보를 확인하기 위해서 아래 명령어를 실행한다.

  ```bash
  $ git config --global -l
  user.email=kang941194@nate.com
  user.name=kang941194
  ```

### gitignore

> 프로젝트를 진행할 때, 개발 환경 혹은 프로젝트 사정 상 git으로 관리될 필요가 없거나 올라가면 안되는 파일이 있다. 이러한 파일들은 `.gitignore`에 입력한다.

* 프로젝트 루트 경로에 위치시키는 것이 기본이지만, 하위 경로에 위치시켜도 하위 경로 기준으로 gitignore 설정이 적용된다.
* 프로젝트를 시작할 때 어떠한 내용을 적어야 할 지 모를 경우 [gitignore.io](https://gitignore.io/)에서 확인한다. 

![image-20200121093627629](images/image-20200121093627629.png)

## 2. 로컬 저장소 활용법

### 2.1 Git 저장소 설정

특정 프로젝트 폴더에서 `git`을 활용하기 위해서 아래 명령어를 실행한다.

```bash
$ git init
Initialized empty Git repository in C:/Users/multicampus/Desktop/강찬엽/ttteeesssttt/.git/
```

* `git init`이 정상적으로 완료되면, 루트 경로에 `.git`이라는 숨김 폴더가 생성된다. 앞으로 모든 `git`관련 동작들은 이 폴더에 기록된다.

* `git bash`에서 `(master)`라는 브랜치 정보가 표기된다.

  ```bash
  multicampus@DESKTOP-KVCQHCD MINGW64 ~/Desktop/강찬엽/ttteeesssttt (master)
  $
  ```

### 2.2 add

> `git`에서 커밋을 하고 싶은 파일을 staging area로 이동시키는 명령어다.

```bash
$ git add a.txt   # 특정 파일을 add -> stage
$ git add images/ # 특정 폴더를 add -> stage
$ git add .       # 모든 파일 및 폴더를 add -> stage
```

### add 이전 상태

추적하고 있지 않은 파일이 있다고 말해주고 있으며, `git add` 명령어를 작성해보라고 권유하기까지 한다.

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

### add 이후 상태 (bash 기준)

add를 한 파일은 초록색 색상으로 커밋할 준비가 되었다고 말해주고 있고, add를 하지 않은 파일은 여전히 빨간 색상으로 추적하지 않는 파일이라고 말해준다.

```bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

따라서 `git` 작업을 할 때, 항상 `git status` 명령어를 통해서 현재 상태를 확인해야 한다.

## 3. Commit

> 실제 `Git`을 통해 이력(버전)을 남기기 위해서는 `커밋(commit)`을 해야한다.

* 커밋을 남길 때는 항상 커밋 메시지를 작성한다. 메시지는 해당 이력에 대한 정보를 가햐지고 있다.

  ```bash
  $ git commit -m "작업 파일 추가" # ""안에 적절한 커밋 메시지를 작성한다.
  [master (root-commit) 3f27e0f] 작업 파일 추가
   2 files changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 a.txt
   create mode 100644 b.txt
  
  ```

* 커밋 이력을 확인하기 위해서는 아래 명령어를 실행한다.

  ```bash
  $ git log
  commit 3f27e0fb2ccbd1a1ac8928e7ad2e959333a07f14 (HEAD -> master)
  Author: kang941194 <kang941194@nate.com>
  Date:   Tue Jan 21 09:49:06 2020 +0900
  
      작업 파일 추가
  ```

* 이후 변경 사항이 발생하면 `add` -> `commit`을 진행한다.

  * `add` : 커밋할 대상 파일을 선정하는 작업
  * `commit` : 이력을 확정하는 작업



## 4. 원격 저장소(Remote Repository) 활용하기

> Git != Github
>
> Git을 기반으로 원격 저장소를 제공해주는 서비스는 다양하다.
>
> 우리는 가장 인기있는 서비스인 Github를 기준으로 활용해보자.

### 4.1 기본 설정

#### 1) 원격 저장소 설정

원격 저장소(remote)를 `origin`이라는 이름으로 `github_URL`을 설정한다.

* origin 말고 원하는 이름을 설정해도 되지만, 일반적으로 origin을 사용한다.

```bash
$ git remote add origin github_URL
```

아래 명령어를 통해 저장된 원격 저장소 목록을 확인할 수 있다.

```bash
$ git remote -v
```

잘못 설정한 경우, 아래 명령어를 통해 삭제 가능하다.

```bash
$ git remote rm origin
$ git remote -v
```



## 4.2 Push

> 원격 저장소에 업로드 하기 위해서 `push` 명령어를 사용한다.

origin으로 설정된 원격 저장소에 push한다(== 업로드한다!).

```bash
$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 23.37 KiB | 23.37 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0)
To https://github.com/kang941194/TIL.git
 * [new branch]      master -> master
```



작업하기 전에 `git pull`, 작업 끝나면 `git push`를 잊지 않도록 하자 :)











 