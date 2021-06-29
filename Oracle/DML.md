# DML

| 종류 | Full Name                    | 예시                                                      |
| ---- | ---------------------------- | --------------------------------------------------------- |
| DML  | Data Manipulation Language   | INSERT(입력), UPDATE(변경), DELETE(삭제), MERGE(병합)     |
| DDL  | Data Definition Language     | CREATE(생성), ALTER(수정), TRUNCATE(잘라내기), DROP(삭제) |
| DCL  | Data Control Language        | GRANT(권한 주기), REVOKE(권한 뻇기)                       |
| TCL  | Transaction Control Language | COMMIT(확정), ROLLBACK(취소)                              |

## 1. INSERT : 입력

* 1행씩 입력하기

  ```plsql
  INSERT INTO talbe [(column1, column2,...)]
  VALUES (value1, value2, ...);
  
  --컬럼 이름 순서대로
  INSERT INTO dept2 (decode, dname, pdept, area)
  VALUES(900, 'temp_1', 1006, 'Temp Area');
  --모든 컬럼에 입력 할 경우 컬럼 이름 생략 가능
  INSERT INTO dept2
  VALUES(9001, 'temp_2', 1006, 'Temp Area');
  ```

* 특정 컬럼에 값을 입력하기

  ```plsql
  INSERT INTO dept2(dcode, dname, pdept)
  VALUES(9002,'temp_3', 1006);
  ```

* 날짜 데이터 입력하기

  ```plsql
  ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD:HH24:MI:SS';
  
  INSERT INTO professor(profno, name, id, position, pay, hiredate)
  VALUES(5001, 'James Bond', 'Love Me', 'a full professor', 500, '2014-10-23');
  ```

* INSERT와 서브 쿼리 사용하여 여러 행 입력하기

  ```plsql
  INSERT INTO professor3
  SELECT * FROM professor;
  ```



## 2. UPDATE : 수정

* UPDATE	

  ```plsql
  UPDATE talbe
  SET column = value
  WHERE = 조건;
  ```

  

## 3. DELETE : 삭제





## 4. MERGE : 병합