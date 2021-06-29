# Constraint 

* 제약조건 : 테이블에 올바른 데이터만 입력 받고 잘못된 데이터는 들어오지 못하도록 컬럼마다 정하는 규칙

| 조건        | 의미                                                         |
| ----------- | ------------------------------------------------------------ |
| NOT NULL    | 이 조건이 설정된 컬럼에는 NULL 값이 입력되지 못하도록 함     |
| UNIQUE      | 이 조건이 설정된 컬럼에는 중복된 값이 입력되지 못하도록 함   |
| PRIMARY KEY | 이 조건은 NOT NULL + UNIQUE의 특징을 가지며, 테이블 내에서 데이터들끼리의 유일성을 보장하는 컬럼에 설정함. 그리고 테이블당 1개만 설정 가능 |
| FOREIGN KEY | 이 조건은 다른 테이블의 컬럼을 참조해서 검사함               |
| CHECK       | 이 조건에서 설정된 값만 입력을 허용하고 나머지는 거부됨      |



* 테이블 생성시에 지정하기

  ```plsql
  CREATE TABLE new_emp1(
  no NUMBER(4),
  CONSTRAINT emp1_no_pk PRIMARY KEY,
  name VARCHAR2(20) CONSTRAINT emp1_name_nn NOT NULL,
  jumin VARCHAR2(13) CONSTRAINT emp1_jumin_nn NOT NULL
  CONSTSRAINT emp1_jumin_uk UNIQUE,
  loc_code NUMBER(1) CONSTRAINT emp1_area_ck CHECK(loc_code<5),
  deptno VARCHAR2(6) CONSTRAINT emp1_deptno_fk REFERENCES dept2(dcode));
  ```

  

