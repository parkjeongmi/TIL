### git repository 공유 연습

1. 브랜치 생성 및 이동

   ```bash
   $ git branch 브랜치이름
   $ git checkout 브랜치이름
   ```

   ```bash
   $ git checkout -b 브랜치이름 #생성과 이동을 동시에 가능
   ```

2. 작업

   `code.` 로 vs code 들어가서 작업 수행

3. add와 push

   ```bash
   git add .
   git commit -m "수정사항"
   git push origin 브랜치이름
   ```

4. pull request

   `compare&pull request`  클릭해서 들어가기

   `create pull request` 로 pull request 생성하기

   `merge pull request` 로 merge 진행하기

   pull request successfully merged and closed 확인 가능

   정상적으로 pull 된 것 확인 가능함.

5. master로 merge 후 Branch 제거하기 

   ```bash
   $ git checkout master #master브랜치로 돌아오기
   $ git merge new #브랜치 merge하기
   $ git branch -d new #브랜치 삭제하기
   ```

