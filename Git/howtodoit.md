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

   ![스크린샷 2021-06-22 오후 9.36.35](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.36.35.png)

3. add와 push

   ```bash
   git add .
   git commit -m "수정사항"
   git push origin 브랜치이름
   ```

   ![스크린샷 2021-06-22 오후 9.38.08](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.38.08.png)

4. pull request

   ![스크린샷 2021-06-22 오후 9.38.27](/Users/jamie/Desktop/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.38.27.png)

   `compare&pull request`  클릭해서 들어가기

   ![스크린샷 2021-06-22 오후 9.39.09](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.39.09.png)

   `create pull request` 로 pull request 생성하기

   ![스크린샷 2021-06-22 오후 9.39.41](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.39.41.png)

   `merge pull request` 로 merge 진행하기

   ![스크린샷 2021-06-22 오후 9.40.14](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.40.14.png)

   ​	pull request successfully merged and closed 확인 가능

   ![스크린샷 2021-06-22 오후 9.42.16](/Users/jamie/Library/Application%20Support/typora-user-images/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.42.16.png)

   정상적으로 pull 된 것 확인 가능함.

5. master로 merge 후 Branch 제거하기 

   ```bash
   $ git checkout master #master브랜치로 돌아오기
   $ git merge new #브랜치 merge하기
   $ git branch -d new #브랜치 삭제하기
   ```

















