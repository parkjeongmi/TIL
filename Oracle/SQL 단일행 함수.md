## SQL 단일행 함수

* 문자 함수

  | 함수명                           | 의미                                          | 사용예                                                       |
  | -------------------------------- | --------------------------------------------- | ------------------------------------------------------------ |
  | INITCAP                          | 첫 글자만 대문자 변환                         | Select name, id,  **INITCAP(id)** from professor; #Jamie     |
  | LOWER                            | 전부 소문자 변환                              | Select name, id,  **LOWER(id)** from professor;  #jamie      |
  | UPPER                            | 전부 대문자 변환                              | Select name, id,  **UPPER(id)** from student; #JAMIE         |
  | LENGTH                           | 문자열 길이                                   | Select name, id,  **LENGTH(id)** from student; #6            |
  | LENGTHB                          | 문자열 길이의 바이트 값 (한글 하나가 3바이트) | Select name, id,  **LENGTHB(id)** from student; #6           |
  | CONTACT                          | 두 문자열 결합해서 출력 (\|\|와 동일)         | Select **contact(name, id)** from student; #select name \|\| id from student; |
  | SUBSTR(문자열, 시작 위치, 개수)  | 특정 문자만 추출                              | SUBSTR('abc', 1, 2) #ab #Select name, **substr(name, 1, 1)** from student; |
  | SUBSTRB(문자열, 시작 위치, 개수) | 특정 바이트만 추출                            | SUBSTRB("한글", 1, 2) #한  #Select name, **substrb(name, 1, 3)** from student; |
  | INSTR(문자열, '특정 문자')       | 특정 문자의 위치                              | SELECT INSTR(TEL,'-')                                        |
  | INSTRB(문자열, '특정 문자')      | 특정 문자의 위치의 바이트 값                  |                                                              |
  | LPAD(문자열, 자리수, 특정 문자)  | 왼쪽으로 특정 문자를 채움                     | SELECT LPAD(ID, 12, '_') from student;                       |
  | RPAD(문자열, 자리수, 특정 문자)  | 오른쪽으로 특정 문자를 채움                   |                                                              |
  | LTRIM(문자열, 특정문자)          | 왼쪽의 특정 문자를 삭제함                     | SELECT LTRIM(TEL, '02') from student;                        |
  | RTRIM(문자열, 특정문자)          | 오른쪽의 특정 문자를 삭제함                   |                                                              |
  | REPLACE(문자열, A,B)             | 문자열에서 A를 B로 치환함                     | SELECT NAME, REPLACE(NAME, SUBSTR(NAME, 2, 1), '*') FROM STUDENT; |

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

  

