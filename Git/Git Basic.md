## Git 기본 명령어

| 기능                  | git 명령어                                  |
| :-------------------- | :------------------------------------------ |
| 새로운 저장소 만들기  | git init                                    |
| 인덱스에 파일 추가    | git add <파일명><br />git add *             |
| 인덱스 내용 확인      | git status                                  |
| 변경내용 확정         | git commit -m “설명”                        |
| 확정 내용 확인        | git log                                     |
| 로컬 저장소 복제      | git clone /로컬/저장소/경로                 |
| 원격 서버 저장소 복제 | git clone 사용자명@호스트:/원격/저장소/경로 |
| 원격 저장소 로컬 등록 | git remote add origin <원격 서버 주소>      |
| 원격 저장소 반영      | git push origin master                      |
| 원격 저장소 가져오기  | git pull origin mater                       |
| 원격 저장소 목록보기  | git remote -v                               |
| 원격 저장소 삭제      | git remote rm origin                        |



## Git 흐름 정리

![](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%209.12.39.png)

### 1. Git basic

#### 로컬 저장소 설정

```bash
$ git init
```

폴더에 git 저장소를 초기화 하면 `.git` 이라는 폴더가 생긴다. (숨긴 폴더)

실제 폴더에서 보고 싶다면 `보기` -> `숨긴 항목` 체크

```bash
$ ls -a
```

### 2. add

* staging area(INDEX)로 옮기는 작업
* Commit (버전으로 확정)하기 전에 머무르는 곳

```bash
$ git status
```

```bash
$ a.txt
$ git add a.txt  #a.txt를 WD -> SA로 옮긴다. (commit하기 위한 대기하는 곳)
$ git status
On branch master

No commits yet

#commit을 하기 위한 변경 사항들
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
#아직 트래킹되지 않은 (SA에 올라가지 않은) 파일
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

#### add 명령어의 사용법

```bash
$ git add . #현재 디렉토리(하위 디렉토리 포함)의 모든 요소를 staging area로 옮긴다.
$ gid add a.txt #특정한 파일만 SA로 올린다.
$ git add folder #특정한 폴더(폴더 내부 파일 포함)만 올린다.
```









* git (로컬 저장소)

  * working directory 

    작업물들이 최초로 존재하는 공간

    git add를 통해 staging area(INDEX)로 이동

  * staging area

    git commit -m "text"를 통해 하나의 버전으로 'commit'

    commit된 new file을 수정하면 modified됨. 다시 add해서 commit 해야 함

* git hub (원격 저장소)

  * "git remote add origin master"로 remote를 등록
  * "git push origin master로 master branch"로 push

_단, git에서 git hub로 자동 동기화되지 않기 떄문에 push가 필요하다_ 



* 기타

  * Esc + : wq + enter

    (wq는 쓰고 나가는 것, q는 나가는 것)

  * 커밋 편집기 변경

    기본 텍스트 편집기인 `vim` 을 `vs code` 로 대체하는 것

    ```bash
    $ git config --global core.editor "code --wait"
    ```

    

    

