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