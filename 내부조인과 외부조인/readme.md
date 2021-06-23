# 요약집 

### 기초
ORDER BY 1 : 칼럼 첫번째를 기준으로 정렬 

### 1. 내부조인
두 테이블에서 뽑아낼 수 있는 칼럼들을 뽑아내는 방식
- 기본형
select (뽑아낼 칼럼명) 
from 뽑아낼 테이블1, 테이블2,
where (둘의 연결고리 칼럼)

- 테이블 3개형
select (뽑아낼 칼럼명) 
from 뽑아낼 테이블1, 테이블2, 테이블3
where (둘의 연결고리 칼럼)
AND (연결고리 칼럼)

*주의 점 
(1) null 값이 있는 행은 조회가 되지 않는다. 
(2) 연결고리 칼럼을 뽑아낼 때에는 어느 테이블꺼를 뽑아낼지를 명시해줘야 한다. 
(3) 3개의 테이블을 할때에는 WHERE문에서 AND를 활용하면 된다. 

### 2. 외부조인
조인 조건을 만족하는 것은 물론 만족하지 않는 데이터(로우)까지 포함해 조회하는 방식

- 조인조건을 만족하지 않는 a의 테이블의 데이터까지 조회시 -> where a.department_id = b.department_id(+)
  %해당 방법은 오라클 전용 문법.
  
### 3. ANSI 조인 
- 내부조인, 외부조인을 ANSI 문법에 맞게 작성한 쿼리
- 내부조인 : INNER JOIN
- 외부조인 : LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 

(1) INNER JOIN 
- 겹친거 뽑아내! => 내부조인과 똑같은 정의 
- 기본형 FROM문과 WHERE문을 INNER JOIN ON문으로 바꾼 것이다.
ex) 
from employees a, departments b
where a.department_id = b.department_id
=> 
from employees a
INNER JOIN departments b
      on a.department_id = b.department_id 
      
(2) LEFT OUTER JOIN 
- 나를 중심으로 했을 때 ON에서 왼쪽에 있는 칼럼을 가진 테이블 애들도 조회를 해줘!

ex) 
from employees a, departments b
where a.department_id = b.department_id(+)
=> 
from employees a
LEFT OUTER JOIN departments b
      on a.department_id = b.department_id

*OUTER는 생략이 가능함. 

(3) RIGHT OUTER JOIN 
- 나를 중심으로 했을 때 ON에서 오른쪽에 있는 칼럼을 가진 테이블 애들도 조회를 해줘!

ex) 
from employees a, departments b
where a.department_id = b.department_id(+)
=> 
from employees a
RIGHT OUTER JOIN departments b
      on a.department_id = b.department_id

*OUTER는 생략이 가능함. 

(4) FULL OUTHER JOIN 
- 거의 안쓰임. 몰라도 되는 정도임. 


(5) 테이블 3개형
select (뽑아낼 칼럼명) 
from 뽑아낼 테이블1
INNER JOIN 테이블2
  ON (둘의 연결고리 칼럼)
INNER JOIN 테이블3
  ON (둘의 연결고리 칼럼)
  
(6) WHERE구문 추가시에는 ON 뒤에 쓴다. 
select (뽑아낼 칼럼명) 
from 뽑아낼 테이블1
INNER JOIN 테이블2
  ON (둘의 연결고리 칼럼)
INNER JOIN 테이블3
  ON (둘의 연결고리 칼럼)
WHERE문 

*주의할 점
- 앞서 말했던 것과 같이, 
- 여러개의 구문을 쓸때, 앞서서 외부조인을 명령을 먼저 했어도 우리는 내부조인이 명령될시, 사용할 수 없다.  

(6) 셀프조인
SELECT a.employee_id
      ,a.first_name || ' ' || a.last_name emp_name
      ,a.manager_id
      ,b.first_name || ' ' || b.last_name manager_name
 FROM employees a
 INNER JOIN employees b
    ON a.manager_id = b.employee_id
ORDER BY 1;

자신의 사수가 누구인지를 확인할때 주로 사용한다. 












