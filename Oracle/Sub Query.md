# Sub Query

* Sub Query

  * WHERE 절에 연산자 오른쪽에 위치해야 하며 반드시 괄호로 묶어야 함.
  * 특별한 경우 (Top-n 분석 등)를 제외하고는 Sub Query 절에 Order by 절이 올 수 없음
  * 단일 행 Sub Query와 다중 행 Sub Query에 따라 연산자를 잘 선택해야 함.

  

* 단일행 Sub Query

  | 연산자 | 의미        |
  | ------ | ----------- |
  | =      | 같다        |
  | <>     | 같지 않다   |
  | >      | 크다        |
  | >=     | 크거나 같다 |
  | <      | 작다        |
  | <=     | 작거나 같다 |

  ```plsql
  select s.name "STUD_NAME", d.dname "DEPT_NAME"
  from student s, department d
  where s.deptno1 = d.deptno and
  s.sdeptno1 = (select deptno1 from student where name = 'Anthony Hopkins');
  ```

  ```plsql
  select name, weight
  from student
  where weight > (select avg(weight) from student where deptno1 = 201);
  ```



* 다중행 Sub Query

  | 연산자 | 의미                                              |
  | ------ | ------------------------------------------------- |
  | IN     | 서브 쿼리 결과와 같은 값을 찾습니다               |
  | EXISTS | Sub Query의 값이 있을 경우 메인 쿼리를 수행합니다 |
  | >ANY   | 서브 쿼리 결과 중에서 최솟값을 반환합니다         |
  | <ANY   | 서브 쿼리 결과 중에서 최댓값을 반환합니다         |
  | <ALL   | 서브 쿼리 결과 중에서 최솟값을 반환합니다         |
  | >ALL   | 서브 쿼리 결과 중에서 최댓값을 반환합니다         |

  ```plsql
  --emp2테이블과 dept2 테이블을 참조하여 근무지역이 포항 본사인 
  select e.empno, e.name, e.deptno
  from emp2 e
  where deptno in (select dcode from dept2 where area = '포항본사');
  ```

  * Exists VS. IN
    * Exists : 단지 해당 row가 존재하는지만 확인하고, 더 이상 수행되지 않음
    * IN : 실제 존재하는 데이터들의 모든 값까지 확인

  ```plsql
  --exists 연산자
  select * from dept
  where exists (select deptno from dept where deptno = &dno);
  
  select * from dept
  where deptno in (select deptno from dept where deptno = &dno);
  
  --student, professor 테이블을 이용하여 담당학생이 없는 교수번호와 교수이름 출력
  select p.profno, p.name
  from professor p
  where not exists (select studno from student where profno =p.profno);
  ```

  ```plsql
  select name, position, to_char(pay, '$999,999,999') "연봉"
  from emp2
  where pay > any(select pay from emp2 where position = '과장');
  ```

  ```plsql
  select name, grade, weight
  from student
  where weight < all (select weight from student where grade=2);
  
  select d.dname, e.name, to_char(e.pay, '$999.999.999') "연봉"
  from emp2 e dept2 d
  where e.pay > any (select avg(pay) from emp2 group by deptno)
  and e.deptno = d.dcode;
  ```



* 다중 컬럼 Sub Query

  ```plsql
  select p.profno, p.name, p.hiredate, d.dname
  from professor p, department d
  where (p.deptno, p.hiredate) in (select deptno, min(hiredate) from professor group by deptno)
  and p.deptno = d.deptno
  order by hiredate;
  ```

  