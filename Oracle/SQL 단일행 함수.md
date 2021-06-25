## SQL 단일행 함수

* 문자 함수

  | 함수명                              | 의미                                          | 사용예                                                       |
  | :---------------------------------- | :-------------------------------------------- | :----------------------------------------------------------- |
  | INITCAP                             | 첫 글자만 대문자 변환                         | Select name, id,  **INITCAP(id)** from professor; #Jamie     |
  | LOWER                               | 전부 소문자 변환                              | Select name, id,  **LOWER(id)** from professor;  #jamie      |
  | UPPER                               | 전부 대문자 변환                              | Select name, id,  **UPPER(id)** from student; #JAMIE         |
  | LENGTH                              | 문자열 길이                                   | Select name, id,  **LENGTH(id)** from student; #6            |
  | LENGTHB                             | 문자열 길이의 바이트 값 (한글 하나가 3바이트) | Select name, id,  **LENGTHB(id)** from student; #6           |
  | CONTACT                             | 두 문자열 결합해서 출력 (\|\|와 동일)         | Select **contact(name, id)** from student; #select name \|\| id from student; |
  | **SUBSTR(문자열, 시작 위치, 개수)** | 특정 문자만 추출                              | SUBSTR('abc', 1, 2) #ab #Select name, **substr(name, 1, 1)** from student; |
  | SUBSTRB(문자열, 시작 위치, 개수)    | 특정 바이트만 추출                            | SUBSTRB("한글", 1, 2) #한  #Select name, **substrb(name, 1, 3)** from student; |
  | **INSTR(문자열, '특정 문자')**      | 특정 문자의 위치                              | SELECT **INSTR(TEL,'-')**                                    |
  | INSTRB(문자열, '특정 문자')         | 특정 문자의 위치의 바이트 값                  |                                                              |
  | LPAD(문자열, 자리수, 특정 문자)     | 왼쪽으로 특정 문자를 채움                     | SELECT **LPAD(ID, 12, '_')** from student;                   |
  | RPAD(문자열, 자리수, 특정 문자)     | 오른쪽으로 특정 문자를 채움                   |                                                              |
  | LTRIM(문자열, 특정문자)             | 왼쪽의 특정 문자를 삭제함                     | SELECT **LTRIM(TEL, '02')** from student;                    |
  | RTRIM(문자열, 특정문자)             | 오른쪽의 특정 문자를 삭제함                   |                                                              |
  | REPLACE(문자열, A,B)                | 문자열에서 A를 B로 치환함                     | SELECT NAME, **REPLACE(NAME, SUBSTR(NAME, 2, 1), '*')** FROM STUDENT; |

  Q. 전화번호(TEL)에서 괄호( ')' ) 앞까지의 지역 번호를 추출하고 싶을 때 ex) 055, 051, 032, 031

  -> ')' 괄호의 위치를 INSTR로 추출한 후, 해당 자리까지를 SUBSTR로 추출하기

  ```plsql
  select substr(tel, 1, instr(tel, ')')-1)
  from student;
  ```

  Q. 전화번호(TEL)의 앞 자리 ex) 032-571-2428 일 경우, '571' 출력

  ```plsql
  select substr(tel, instr(tel, ')')+1,(instr(tel, '-')- instr(tel,')')-1))       
  from student;
  ```

  Q. 전화번호(TEL)의 뒷 자리 ex) 032-571-2428 일 경우, '2428' 출력

  ```plsql
  select substr(tel, instr(tel, '-')+1, 4)       
  from student;
  ```

  Q. 전화번호(TEL)에 의해 서울에 사는 학생 출력

  ```plsql
  Select name, tel
  from student
  Where substr(tel, 1, instr(tel, ')')-1) = '02';
  ```

  Q. 이름 가운데 글자 별 표시로 가명처리 ex) 홍길동 -> 홍*동

  ```plsql
  SELECT NAME, REPLACE(NAME, SUBSTR(NAME, 2, 1), '*') "가명처리" FROM STUDENT;
  ```

  

* 숫자 관련 함수

  |      이름      |            의미             |         사용예         |
  | :------------: | :-------------------------: | :--------------------: |
  | ROUND(숫자, m) |           반올림            | ROUND(12.345,2) #12.35 |
  |     TRUNC      |            버림             | TRUNC(12.345,2) #12.34 |
  |      MOD       |           나머지            |     MOD(12,10) #2      |
  |      CEIL      |  가장 근접한 큰 정수(올림)  |    CEIL(12.345) #13    |
  |     FLOOR      | 가장 근접한 작은 정수(버림) |   FLOOR(12.345) #12    |
  |     POWER      |   숫자1의 숫자 2승을 출력   |     POWER(3,2) #9      |

  * 반올림 절사 규칙 = 소수점 '.' 기준

    * m의 숫자가 양수 = 소수점 기준 우측 m번째까지 보여줌 ex) round(192.153,1) #192.2
    * m의 숫자가 음수 = 소수점 기준 왼쪽 m번째에서 반올림 ex) round(192.153, -1) #190

    

* 날짜 관련 함수

  | 함수명                             | 의미                               | 결과 |
  | ---------------------------------- | ---------------------------------- | ---- |
  | SYSDATE                            | 시스템의 현재 날짜와 시간          | 날짜 |
  | MONTHS_BETWEEN(최근날짜, 과거날짜) | 두 날짜 사이의 개월 수             | 숫자 |
  | ADD_MONTHS(날짜, 더할 개월)        | 주어진 날짜에 개월을 더함          | 날짜 |
  | NEXT_DAY(날짜, 다음 날짜)          | 날짜를 기준으로 돌아오는 날짜 출력 | 날짜 |
  | LAST_DAY(날짜)                     | 그 달의 마지막 날짜                | 날짜 |
  | TRUNC(날짜)                        | 주어진 날짜 버림                   | 날짜 |

  * 날짜 형식을 지정해서 출력

    ALTER SESSION SET NLS_DATE_FORMAT = 'YY/MM/DD';

  * MONTHS_BETWEEN은 '-'로 마이너스 한 것과 유사 => 단, 개월로 출력됨

    ROUND(최근날짜-과거날짜) => 단, 날짜로 출력됨

  

* 형 변환 함수

  | 데이터 타입                   | 설명                             |
  | ----------------------------- | -------------------------------- |
  | CHAR(n)                       | 고정길이의 문자 저장             |
  | **VARCHAR2(n)**               | 변하는 길이의 문자               |
  | **NUMBER(소수점자리수,크기)** | 숫자 값 저장                     |
  | **DATE**                      | 날짜 저장                        |
  | BLOB                          | 가변 길이의 바이너리 데이터 저장 |
  | LONG                          | 가변 길이의 문자 저장 (2GB)      |
  | CLOB                          | 가변 길이의 문자 저장 (4GB)      |

  * to_number('바꿀 숫자')

    select 2 + to_number('2') from dual; #4

  * to_date('바꿀 문자')

  * to_char('바꿀 숫자 혹은 문자')

    Select months_between(sysdate, '98/06/08') from dual; #자동으로 형변환 해줌

    Select sysdate - to_date('98/06/08') from dual; #직접 형변환 해야함

    * to_date 활용

      select birthday, to_char(birthday, 'YYYY'), to_char(birthday, 'MM')  from student;

      select name, birthday from student where to_char(birthday, 'MM') = '05';

  * RR

    00~49에서는 20xx 반환

    50~99에서는, rr는 19xx / yy는 20xx 반환

  * to_char함수

    | 종류 | 의미                    | 사용예                   | 결과    |
    | ---- | ----------------------- | ------------------------ | ------- |
    | 9    | 9의 개수만큼 자리수     | to_char(1234,'99999')    | 1234    |
    | 0    | 빈자리를 0으로 채움     | to_char(1234,'099999')   | 001234  |
    | $    | $ 표시를 붙여서 표시    | to_char(1234, '$9999')   | $1234   |
    | ₩    | ₩ 표시를 붙여서 표시    | to_char(1234, 'l9999')   | ₩1234   |
    | .    | 소수점 이하를 표시      | to_char(1234, '9999.99') | 1234.00 |
    | ,    | 천 단위 구분기호를 표시 | to_char(12345, '99,999') | 12,345  |
  
  * ASCII('A')
  
  

* 일반 함수

  * NVL(컬럼, 치환할 값) : NULL 값을 만나면 다른 값으로 치환해서 출력

    * NVL(sal, 0) #sal이 null이면 0으로 치환

      ```plsql
      Select profno, name, pay, nvl(bonus,0), to_char(pay*12+nvl(bonus, 0), '99,999') "TOTAL"
      from professor
      where deptno=201;
      ```

  * NVL2(컬럼, null이면 치환할 값1, null이 아니면 치환할 값2)

    ```plsql
    Select empno, ename, sal, nvl2(comm, sal+comm, sal*0) "NVL2"
    from emp
    where deptno = 30
    
    Select empno, ename, to_nvl2(comm, 'Exist', 'NULL')
    from emp
    where deptno = 30;
    ```

  * DECODE(A, B, '1', null) #A가 B일 경우 '1' 출력 (null은 생략 가능)

    ```plsql
    select deptno, name, decode(deptno, 101, 'Computer Engineering') "DNAME"
    from professor;
    ```

    * DECODE 중첩

    ```plsql
    select deptno, name, decode(deptno, 101, decode(name,'조인형','BEST!',' '),' ') "ETC"
    from professor;
    ```

    ```plsql
    select name, jumin, decode(substr(jumin, 7, 1), '1','MAN','WOMAN') "Gender"
    from student
    where deptno1 = 101;
    ```

    ```plsql
    select name, tel, decode(substr(tel, 1, instr(tel, ')')-1),'02','SEOUL','031','GYENGGGI','05','BUSAN','052','ULSAN','055','GYEONGNAM',' ') "LOC"
    from student
    where deptno1 = 101;
    ```

    

  * CASE 문

    * CASE 조건 WHEN 결과1 THEN 출력1

      [WHEN 결과2 THEN 출력2]

      ELSE 출력3

      END "컬럼명"

    ```plsql
    SELECT NAME, SUBSTR(JUMIN,3,2) "MONTH", 
    CASE WHEN  SUBSTR(JUMIN,3,2) BETWEEN '01' AND '03' THEN '1/4'
    WHEN SUBSTR(JUMIN,3,2) BETWEEN '04' AND '06' THEN '2/4'
    WHEN SUBSTR(JUMIN,3,2) BETWEEN '07' AND '09' THEN '3/4'
    ELSE '4/4'
    END "Qua"
    FROM STUDENT
    ORDER BY "Qua";
    ```

    ```plsql
    select empno, ename, sal, 
    case when sal <= 1000 then 'Level 1'
    when sal<= 2000 then 'Level 2'
    when sal <= 3000 then 'Level 3'
    when sal <= 4000 then 'Level 4'
    else 'Level 5'
    end "LEVEL"
    from emp
    order by "LEVEL" desc;
    ```

    
