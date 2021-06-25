## JOIN

* JOIN 개념

  각 테이블간에 공통된 컬럼으로 데이터를 합쳐 표현하는 것.

  ```plsql
  --Oracle join
  SELECT e.ename, d.dname
  from emp e, dept d
  where e.deptno = d.deptno;
  ```

  ```plsql
  --Ansi join
  select e.ename, d.dname
  from emp e inner join dept d
  on e.deptno=deptno;
  ```

  ```plsql
  --교수명과 교수가 속한 학과 출력
  select p.name, d.dname
  from professor p, department d
  where p.deptno = d.deptno;
  ```

* JOIN의 종류

  | 방법                     | 의미                                                         |
  | ------------------------ | ------------------------------------------------------------ |
  | EQUIJOIN(등가조인)       | 두 개의 테이블 간에 컬럼값들이 **정확하게 일치하는 경우** 사용 |
  | NON-EQUIJOIN(비등가조인) | 두 개의 테이블 간에 컬럼값들이 서로 정확하게 일치하지 않는 경우에 사용 |
  | OUTER JOIN               | 두 개의 테이블 간에 JOIN을 걸었을 경우, JOIN의 조건을 만족하지 않는 경우에도 **그 데이터들을 보고자 하는 경우**에 (+)연산자를 사용해 조인 |
  | SELF JOIN                | 두 개의 테이블들간에 JOIN을 거는 것이 아니라 **같은 테이블에 있는 행들을 JOIN**하는데 사용 |

  ```plsql
  --학생번호, 학생명, 담당교수번호, 담당교수이름 출력
  select s.studno 학생번호, s.name 학생명, s.profno 담당교수번호, p.name 담당교수이름
  from student s, professor p
  where s.profno = p.profno;
  ```

  