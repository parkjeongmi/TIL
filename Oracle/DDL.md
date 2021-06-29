# DDL

| 종류 | Full Name                    | 예시                                                      |
| ---- | ---------------------------- | --------------------------------------------------------- |
| DML  | Data Manipulation Language   | INSERT(입력), UPDATE(변경), DELETE(삭제), MERGE(병합)     |
| DDL  | Data Definition Language     | CREATE(생성), ALTER(수정), TRUNCATE(잘라내기), DROP(삭제) |
| DCL  | Data Control Language        | GRANT(권한 주기), REVOKE(권한 뻇기)                       |
| TCL  | Transaction Control Language | COMMIT(확정), ROLLBACK(취소)                              |

## 1. CREATE : 생성

* 일반 테이블 생성하기

  ```plsql
  CREATE TABLE new_table(
  no NUMBER(3),
  name VARCHAR2(10),
  birth DATE);
  ```

* 기본 입력 값을 설정하면서 생성하기

  ```plsql
  CREATE TABLE tt02(
  no number(3,1) DEFAULT 0,
  name VARCHAR2(10) DEFAULT 'No Name')
  hiredate DATE DEFAULT SYSDATE);
  
  INSERT INTO tt02 (no) VALUES(1);
  ```

* 테이블 복사하기

  ```plsql
  --모든 컬럼 다 복사하기
  CREATE TABLE dept3
  AS
  SELECT * FROM dept2;
  
  --특정 컬럼만 복사하기
  CREATE TABLE dept4
  AS
  SELECT decode, dname
  FROM dept2;
  
  --테이블 구조(컬럼)만 가져오고 데이터 안 가져오기
  CREATE TABLE dept5
  AS
  SELECT * FROM dept2
  WHERE 1 = 2;
  ```

## 2. ALTER 명령

* 새로운 컬럼 추가하기

  ```plsql
  ALTER TABLE dept6
  ADD(location VARCHAR2(10));
  ```

* 컬럼 추가하면서 기본 값 지정하기

  ```plsql
  ALTER TABLE dept6
  ADD(location2 VARCHAR2(10) DEFAULT 'SEOUL');
  ```

* 테이블의 컬럼 이름 변경하기

  ```plsql
  ALTER TABLE dept6 RENAME COLUMN location2 TO loc;
  ```

* 컬럼의 데이터 크기 조정하기

  ```plssql
  ALTER TABLE dept7
  MODIFY(loc VARCHAR2(20));
  ```

## 3-4. TRUNCATE & DROP

```plsql
--CASCADE CONSTRAINTS
ALTER TABLE dept7 DROP COLUMN loc CASCADE CONSTRAINTS;

--TRUNCATE
TRUNCATE TABLE dept7;

--DROP
DROP TABLE dept7;
```

