# 0nd_week

## Subquery

- 15.2.15. SubquerieS
    - **Subquery**는 다른 query 안에 포함된 SELECT query
    - `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `SET`, `DO` 문 안에서 사용 가능
    - 일반적으로 괄호 `()`로 감싸며, 서브쿼리가 먼저 평가
    - **Correlated subquery**는 outer query의 column을 참조하고, 각 row마다 실행
- 15.2.15.2. Comparisons Using Subqueries
    - Subquery는 `=`, `!=`, `>`, `<`, `>=`, `<=` 등 비교 연산자와 함께 사용될 수 있음
    - subquery가 **단일 값 (scalar)** 을 반환해야 함. 그렇지 않으면 error 발생
        
        ```sql
        sql
        CopyEdit
        SELECT name FROM employees WHERE salary = (SELECT MAX(salary) FROM employees);
        ```
        
    - 만약 서브쿼리가 여러 값을 반환하면 error: `Subquery returns more than 1 row`
- 15.2.15.3. Subqueries with ANY, IN or SOME
    - **multi-row subqueries**에 사용됨.
    
    ### `IN`
    
    - 값이 서브쿼리 결과 중 하나라도 일치하면 true
        
        ```sql
        sql
        CopyEdit
        SELECT name FROM employees WHERE dept_id IN (SELECT id FROM departments);
        ```
        
    
    ### `ANY` / `SOME`
    
    - 비교 조건이 서브쿼리의 **어느 하나**라도 만족하면 true
        
        ```sql
        sql
        CopyEdit
        SELECT name FROM employees WHERE salary > ANY (SELECT salary FROM employees WHERE dept_id = 3);
        ```
        
        → "3번 부서 중 가장 낮은 급여보다 높은 급여를 받는 직원"
        
- 15.2.15.4. Subqueries with ALL
    - 비교 조건이 서브쿼리 결과의 **모든 값**을 만족해야 true
        
        ```sql
        sql
        CopyEdit
        SELECT name FROM employees WHERE salary > ALL (SELECT salary FROM employees WHERE dept_id = 3);
        ```
        
        → 이건 "3번 부서 모든 사람보다 급여가 높은 직원"을 의미.
        
    - `ALL`은 항상 전체 조건을 만족해야 하기 때문에 일반적으로 더 제한적
- 15.2.15.6. Subqueries with EXISTS or NOT EXISTS
    - **EXISTS**는 서브쿼리 결과가 **하나라도 존재하면** true
    - **NOT EXISTS**는 서브쿼리 결과가 **없으면** true
        
        ```sql
        sql
        CopyEdit
        SELECT name FROM employees e
        WHERE EXISTS (SELECT 1 FROM departments d WHERE d.id = e.dept_id AND d.name = 'Sales');
        ```
        
    - EXISTS는 단순히 **row 존재 여부**만 평가하므로 성능적으로 효율적
    - 일반적으로 correlated subquery 형태로 사용
- 15.2.15.10. Subquery Errors

### 📝 문제 풀이:

- 🔗 [Solvesql - 많이 주문한 테이블](https://solvesql.com/problems/find-tables-with-high-bill/)
    
    ```sql
    SELECT *
    FROM tips
    WHERE total_bill > (SELECT AVG(total_bill) FROM tips);
    ```
    
- 🔗 [Solvesql - 레스토랑의 대목](https://solvesql.com/problems/high-season-of-restaurant/)
    
    ```sql
    sql
    CopyEdit
    SELECT day
    FROM tips
    GROUP BY day
    HAVING AVG(total_bill) > (SELECT AVG(total_bill) FROM tips);
    ```
    

## WITH (Common Table Expressions, CTE)

- `WITH`는 Common Table Expression (CTE) 을 정의할 때 사용
- CTE는 일시적인 이름 있는 result set으로, `SELECT`, `INSERT`, `UPDATE`, `DELETE` 쿼리에서 사용 가능
- view처럼 사용되지만, 일회성이고 쿼리 범위 내에서만 유효

### Syntax

```sql
sql
CopyEdit
WITH cte_name [(column1, column2, ...)] AS (
    subquery
)
SELECT * FROM cte_name;
```

- 괄호 속 column list는 생략 가능하지만 명확하게 정의
- 하나의 쿼리에서 여러 개의 CTE도 선언 가능

```sql
sql
CopyEdit
WITH cte1 AS (...), cte2 AS (...) SELECT ...
```

## 주요 특징

- **재사용성**: 동일한 서브쿼리를 여러 번 참조할 경우 CTE로 정의
- **가독성 향상**: 복잡한 쿼리를 단계별로 분리해서 명확하게 표현 가능
- **CTE 안에서 다른 CTE 참조 가능**: 순차적으로 선언되면 앞에 선언된 CTE를 뒤에서 사용 가능

### 📝 문제 풀이:

🔗 [programmers - 식품분류별 가장 비싼 식품의 정보 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/131116)

```sql
sql
CopyEdit
WITH MaxPricePerArea AS (
    SELECT AREA, MAX(PRICE) AS MAX_PRICE
    FROM REST_INFO
    WHERE FOOD_TYPE = '일식'
    GROUP BY AREA
)

SELECT R.AREA, R.REST_NAME, R.FOOD_TYPE, R.PRICE
FROM REST_INFO R
JOIN MaxPricePerArea M
  ON R.AREA = M.AREA AND R.PRICE = M.MAX_PRICE
WHERE R.FOOD_TYPE = '일식'
ORDER BY R.AREA ASC, R.PRICE DESC;

```