## SQL 복수행 함수

* 복수행 함수

| 함수이름 | 의미       | 사용예     |
| -------- | ---------- | ---------- |
| COUNT    | 총 건수    | COUNT(sal) |
| SUM      | 합계       | SUM(sal)   |
| MAX, MIN | 최대, 최소 | MAX(sal)   |
| AVG      | 평균       | AVG(sal)   |

* 날짜

  * 최신 날짜가 큼 / 과거 날짜가 작음
  * MAX(날짜) = 최신
  * MIN(날짜) = 과거

* GROUP BY

  * GROUP BY 절에 오는 것만 SELECT 절에 올 수 있음

    ```plsql
    select deptno, round(avg(pay))
    from professor
    group by deptno
    order by 1;
    ```

    ```plsql
    select position "pos", round(avg(nvl(pay,0))) "avg", max(pay) "max", min(pay) "min"
    from professor
    group by position
    order by "avg";
    ```

  * ORDER BY 1 #첫 번째 column으로 정렬

  * GROUP BY DEPTNO, JOB #DEPTNO와 JOB이 같은 것들로 그룹화함

    ```plsql
    select position "pos", deptno "dep", round(avg(nvl(pay,0))) "avg"
    from professor
    group by deptno, position
    order by 2;
    ```

  * HAVING

    ```plsql
    SELECT deptno, AVG(NVL(sal,0))
    FROM emp
    WHERE deptno > 10
    GROUP BY deptno
    HAVING AVG(NVL(sal,0))>2000;
    ```

    ```plsql
    select grade, round(avg(nvl(height,0))) "height", round(avg(nvl(weight,0))) "weight"
    from student
    group by grade
    having round(avg(nvl(height,0))) < 170;
    ```

* 집계용 함수

  * ROLLUP : 소계와 합게를 구해주는 함수

    * GROUP BY에만 쓸 수 있음

    * UNION ALL과의 차이

    ```plsql
    --부서와 직급별) 평균급여와 사원수
    select deptno, job, round(avg(nvl(sal,0))) "평균급여", count(*)"사원수"
    from emp
    group by deptno, job
    union all
    
    --부서별) 평균급여와 사원수
    select deptno, null job, round(avg(nvl(sal,0))) "평균급여", count(*) "사원수"
    from emp
    group by deptno
    union all
    
    --전체) 평균급여와 사원수
    select null deptno, null job, round(avg(nvl(sal,0))) "평균급여", count(*) "사원수"
    from emp
    order by 1,2;
    ```

    * ROLLUP 활용

    ```plsql
    select deptno, job, round(avg(nvl(sal,0))) avg, count(*) cnt
    from emp
    group by rollup(deptno, job);
    ```

  * CUBE  : 소계와 전체 합계까지 출력하는 함수

  * GROUPING SETS

  * RANK : 순위 출력 함수

    * RANK(조건값) WITHIN GROUP

      ORDER BY 조건 값 컬럼명 [ASC/DESC]

    ```plsql
    SELECT RANK('SMITH') WITHIN GROUP
    (ORDER BY ename) "RANK"
    FROM EMP;
    ```

    ```plsql
    SELECT RANK(2450) WITHIN GROUP
    (ORDER BY sal) "RANK"
    FROM EMP;
    ```

    * partition by : group by와 동일하게 그룹지어 결과를 출력
    * order by : partition by로 정의된 것 내에서 행들의 정렬 순서를 정의

    ```plsql
    --professor 테이블에서 직급별 급여 순위 출력
    select profno, name, position, pay,
    rank() over (partition by position order by pay desc) "rank"
    from professor;
    ```

    ```plsql
    --emp 테이블에서 같은 부서 내 job별로 급여 순위 출력
    select empno, ename, sal, deptno,job,
    rank() over (partition by deptno, job order by sal desc) "rank"
    from emp;
    ```

  * ROW_NUMBER() 

  * Sum() over

    ```plsql
    --panmae 테이블에서 대리점별 판매액을 누적하여 출력
    select p_store "대리점", p_total "판매액", sum(p_total) over (partition by p_code order by p_code) "누적 판매액"
    from panmae;
    ```

    ```plsql
    select p_code 제품코드, p_store 판매점, p_date 판매날짜, p_qty 판매량, p_total 판매금액,
    sum(p_total) over (partition by p_code, p_store order by p_total) 누적판매금액
    from panmae;
    ```