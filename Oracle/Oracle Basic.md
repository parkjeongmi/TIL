# Oracle

Oracle 기본 명령어

* 사용자 조회하기

  ```plsql
  SELECT *
  FROM ALL_USERS;
  --모든 사용자를 조회한다
  ```

* 사용자 생성하기

  ```plsql
  CREATE USER 홍길동
  IDENTIFIED BY 비밀번호;
  --'홍길동'이라는 계정을 만들고 비밀번호는 '비밀번호'이다.
  ```

* 사용자 권한주기

  ```plsql
  GRANT 권한1, 권한2, 권한3 TO 홍길동;
  --'홍길동'에게 권한1, 권한2, 권한3을 줘라
  GRANT CONNECT, RESOURCE, DBA TO 홍길동;
  --'홍길동'에게 접속 권한, 저장소 권한, 관리자 권한을 줘라
  ```

* 사용자 권한뺏기

  ```plsql
  REVOKE 권한1, 권한2, 권한3 FROM 홍길동;
  --'홍길동'에게 권한1, 권한2, 권한3을 뺏어라
  ```

* 테이블 정보 조회하기

  ```plsql
  DESC 테이블명
  --테이블명을 조회하라
  ```

* 테이블 조회하기

  ```plsql
  SELECT *
  FROM TABS;
  --모든 테이블을 조회한다
  ```

* 테이블 생성하기

  ```plsql
  CREATE TABLE NEW
  {
  A VARCHAR2(20),
  B VARCHAR2
  C NUMBER
  };
  --NEW라는 테이블을 생성해라.
  --컬렘헤더는 VARCHAR2 자료형의 A, B
  --NUMBER 자료형의 C이다.
  ```

* 데이터 조회하기

  ```plsql
  SELECT A
  FROM NEW
  WHERE NAME='jamie';
  --NEW라는 테이블에서 NAME의 값이 jamie인 A를 조회해라
  ```

* 데이터 생성하기

  ```plsql
  INSERT INTO NEW
  VALUES('NAME', 'JOB', 'SAL');
  --NEW라는 테이블에 'NAME', 'JOB', 'SAL' 데이터를 생성하라
  ```

* 원하는 조건 골라내기

  ```plsql
  SELECT JOB, SAL
  FROM EMP
  WHERE NAME = 'jamie';
  --이름이 jamie인 조건의 JOB, SAL을 조회하라
  ```

  ```plsql
  SELECT *
  FROM EMP
  WHERE HIREDATE BETWEEN '81/01/01' AND '81/12/31';
  ```

* 컬럼 병합하기

  ```plsql
  SELECT FIRST_NAME || ' ' || LAST_NAME 이름
  FROM EMPLOYEES;
  ```

  ```plsql
  SELECT ENAME || '''s sal is $' || SAL "Name and Sal"
  
  FROM EMP;
  ```

* 연산자

  |      연산자 종류      | 설명                                          |
  | :-------------------: | --------------------------------------------- |
  |        <>, !=         | 같지 않다                                     |
  |    BETWEEN A AND B    | A와 B 사이에 있다 (이상, 이하)                |
  |      IN (A,B,C)       | A이거나 B이거나 C                             |
  |         LIKE          | 특정 패턴이 있는 조건 검색                    |
  |      LIKE '박%'       | 글자수 제한 없음 ex) 박% => 박정미, 박정정    |
  |      LIKE '박_'       | 한 글자 제한 ex) 박_ => 박정, 박미, 박하 검색 |
  | IS NULL / IS NOT NULL | Null 값(혹은 아닌 값) 검색                    |

* ORDER BY (정렬)

  ```plsql
  select *
  from student
  order by depno asc, name desc;
  --student table를 depno의 오림차순으로 정렬한 후 name 순으로 내림차순 정렬
  ```

* UNION (합집합)

  두 개의 SELECT 결과 합침

  *매칭되는 column의 **type**이 같아야 함*

  ```plsql
  select profno, name, depno, 1 from professor where deptno=101
  union all
  select studno, name, deptno1, 2 from student where deptno1=101;
  --합집합 출력 (학생이면 1, 교수면 2로 열 추가함)
  ```

  * **UNION**은 결과를 합칠 때 중복되는 행은 하나만 표시 (**정렬**도 하고 **중복도 제거**)
  * **UNION ALL**은 중복 제거 하지 않고 모두 합칠 때 표시 (보이는 그대로)

* INTERSECT (교집합)

  ```plsql
  select studno, name from student where deptno1=101
  intersect
  select studno, name from student where deptno2=201;
  --교집합 출력
  ```

* MINUS (차집합)

  ```plsql
  select studno, name from student where deptno1=101
  minus
  select studno, name from student where deptno2=201;
  --차집합 출력
  ```

* DISTINCT (중복제거)

  ```plsql
  select distinct studno, name from student where deptno1=101;
  --studno, name 두 컬럼 모두 중복 제거하고 출력
  ```

* 기타

  * 큰 따옴표는 띄어쓰기, 작은 따옴표는 문자열

  * 날짜는 홑 따옴표 사용

