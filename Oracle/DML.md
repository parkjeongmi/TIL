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

  ```plsql
  --emp2 테이블에서 직위가 없는 사람들의 직위를 '사원'으로 변경
  UPDATE emp2
  SET POSITION = '사원'
  WHERE POSITION IS NULL;
  
  --emp2 테이블에서 직위가 '인턴직'인 사람의 급여를 10% 인상
  UPDATE emp2
  SET PAY = PAY * 1.1
  WHERE EML_TYPE = '인턴직';
  ```

  

## 3. DELETE : 삭제

* DELTE

  ```plsql
  DELTE FROM table
  WHERE 조건;
  ```

  ```plsql
  DELTE FROM dept2
  WHERE decode >= 9000 AND decode <= 9999;
  ```

  

## 4. MERGE : 병합

* MERGE

  ```plsql
  MERGE INTO Table1
  USING Table2
  ON (병합 조건절)
  WHEN MATCHED THEN
  UPDATE SET 업데이트 내용
  DELETE WHERE 조건
  WHEN NOT MATCHED THEN
  INSERT VALUES(컬럼 이름);
  ```

  ```plsql
  create table charge_01(
  u_update varchar2(6),
  cust_no number, 
  u_time number,
  charge number);
  
  create table charge_02(
  u_update varchar2(6),
  cust_no number, 
  u_time number,
  charge number);
  
  insert into charge_01 values('141001', 1000, 2, 1000);
  insert into charge_01 values('141001', 1001, 2, 1000);
  insert into charge_01 values('141001', 1002, 2, 1500);
  insert into charge_01 values('141002', 1000, 3, 1500);
  insert into charge_01 values('141002', 1001, 4, 2000);
  insert into charge_01 values('141002', 1003, 1, 500);
  
  --charge_01 에 charge_02 병합하기
  MERGE INTO charge_01 c1
  USING charge_02 c2
  ON c1.u_update = c2.u_update
  WHEN  MATCHED THEN
  UPDATE SET c1.cust_no = c2.cust_no
  WHEN NOT MATCHED THEN
  INSERT VALUES (c2.u_update, c2.cust_no, c2.u_time, c2.charge);
  
  --charge_01에 charge_02 병합하기
  --병합 조건 : cust_no가 같으면 charge_02 데이터로 갱신
  --같지 않으면 charge_02 삽입
  merge into charge_01 c1
  using charge_02 c2
  on (c1.cust_no = c2.cust_no)
  when matched then
  update set c1.u_update = c2.u_update,
  c1.u_time = c2.u_time
  c1.charge=c2..charge
  when not matched then
  INSERT VALUES (c2.u_update, c2.cust_no, c2.u_time, c2.charge);
  ```

  

#### 연습문제

```plsql
--professor 테이블에서 profno가 3000번 이하인 교수들의 profno, name, pay를 가져와서 professor4 테이블에 한꺼번에 입력하는 쿼리를 쓰세요. (ITAS 방법)

create table professor4
as select profno, name, pay from professor where 1=2;

insert into professor4
select profno, name, pay
from professor
where profno<= 3000;
```

```plsql
--professor 테이블에서 '김현정' 교수의 Bonus를 100만원으로 인상하세요.
update professor
set bonus = 100
where name = '김현정';
```

```plsql
--표준 SQL 문장을 작성하세요.
create table member2(
id char(20) PRIMARY KEY,
height number(10,2) default 0.00);

insert into member2 values('hong', 173.5);
update member2 set height = 180 where id = 'hong';
select height from member2 where id = 'hong';
delete from member2 where height = 180;
```

