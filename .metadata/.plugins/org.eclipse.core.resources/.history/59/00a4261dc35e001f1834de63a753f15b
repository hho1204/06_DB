SELECT FLOOR(AVG(SALARY))
FROM EMPLOYEE;

-- 2) 직원들중 급여가 4091140원 이상인 사원들의 사번, 이름, 직급코드, 급여 조회
SELECT EMP_ID, EMP_NAME, JOB_CODE, SALARY
FROM EMPLOYEE
WHERE SALARY >= 4091140;
     (SELECT FLOOR(AVG(SALARY))
     FROM EMPLOYEE);
     
/*************************************************/
-- 기본적으로 "서브 쿼리"를 먼저 해석!!!!
 --> 서브쿼리 결과를 이용해서 "메인 쿼리 " 해석!!!
    
-- 단, 상호연관 서브쿼리는 순서가 반대!!(메인 -> 서브)

/*************************************************/
--SELECT 
--FROM EMPLOYEE
--JOIN JOB USING(JOB_CODE)
--LEFT JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)
--WHERE SALARY > SUM(SALARY);
    
-- 가장 적은 급여를 받는 직원의
-- 사번, 이름, 직급명, 부서코드, 급여, 입사일을 조회 
SELECT EMP_ID, EMP_NAME, JOB_NAME, DEPT_CODE, SALARY, HIRE_DATE   
FROM EMPLOYEE
JOIN JOB USING(JOB_CODE)
WHERE SALARY =
			(SELECT MIN(SALARY) FROM EMPLOYEE);

-- 노옹철 사원의 급여보다 많이 받는 직원의
-- 사번, 이름, 부서명, 직급명, 급여를 조회
SELECT EMP_ID, EMP_NAME, JOB_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
JOIN JOB USING(JOB_CODE)
JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)
WHERE SALARY >
      (SELECT SALARY FROM EMPLOYEE WHERE EMP_NAME = '노옹철');
      
-- 부서별(부서가 없는 사람 포함) 급여의 합계 중 
-- 부서명, 급여 합계를 조회
     
-- 2) 부서별 급여합이 21760000원 부서의 부서명과 급여 합 조회
SELECT DEPT_TITLE, SUM(SALARY)
FROM EMPLOYEE
LEFT JOIN DEPARTMENT ON(DEPT_CODE = DEPT_ID)
GROUP BY DEPT_TITLE
HAVING SUM(SALARY) = 21760000;

/* GROUP BY에 작성된 컬럼명만 SELECT절에 작성할 수 있다!!!  */





-- 부서별 인원 수가 3명 이상인
-- 부서명, 인원 수 조회
SELECT DEPT_TITLE, COUNT(*)
FROM EMPLOYEE
LEFT JOIN DEPARTMENT ON (DEPT_CODE = DEPT_ID)
GROUP BY DEPT_TITLE;

-- 부서별 인원 수가 가장 적은 부서의
-- 부서명, 인원수 조회
SELECT
		NVL(DEPT_TITLE, '없음') "부서명",
		COUNT(*)
FROM EMPLOYEE
LEFT JOIN DEPARTMENT
		ON (DEPT_CODE = DEPT_ID)
GROUP BY DEPT_TITLE
HAVING COUNT(*) =
    (SELECT MIN(COUNT(*))
    FROM EMPLOYEE
    GROUP BY DEPT_CODE);
    
/***** 서브쿼리에서 사용한 별칭을 메인 쿼리에서 사용하기 *****/
-- 인라인뷰 : FROM절에 사용된 서브쿼리
    --> 서브쿼리 결과가 테이블 처럼 인식
   
SELECT 이름, 급여
FROM (SELECT EMP_NAME 이름, SALARY 급여
			FROM EMPLOYEE)
WHERE 급여 >= 4000000;
     -- 메인쿼리 해석 1순위인 FROM절에 작성된
     -- 서브쿼리 결과 컬럼명이 "급여"이기 때문에
     
     -- 메인쿼리 해석 2순위인 WHERE
     -- 메인쿼리 해석 3순위인 SELECT절에서도
     -- 똑같이 "급여"라고 컬럼명을 작성해야 한다!!

---------------------------------------------------