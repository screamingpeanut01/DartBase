# 1st_week

## Window Functions Usage

- **Window function**은 SQL 결과 집합의 **row group(=window)** 을 기준으로 각 row에 계산된 값을 반환하는 함수
- 기존의 **GROUP BY + aggregate functions** 와 달리, row 단위로 결과를 유지하면서 누적/순위 등을 계산 가능

### Syntax

```sql
sql
CopyEdit
function_name(...) OVER (
    [PARTITION BY expr_list]
    [ORDER BY expr_list]
    [frame_clause]
)
```

- **PARTITION BY**: window를 그룹화함 (optional)
- **ORDER BY**: 순서를 정의 (optional)
- **frame_clause**: 계산 범위를 지정 (optional, 일부 함수에서만 사용)

### 예시

```sql
sql
CopyEdit
SELECT name, department, salary,
       RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM employees;
```

같은 부서 내에서 급여 순으로 랭킹

### Window vs Aggregate

| Feature | Aggregate Function | Window Function |
| --- | --- | --- |
| Output Rows | 줄어듦 (집계됨) | 그대로 유지됨 |
| Example | `SUM(salary)` | `SUM(salary) OVER (...)` |

### Frame Clause

- 사용 가능한 옵션:
    - `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`
    - `RANGE BETWEEN ...`
    - `GROUPS BETWEEN ...`
- 기본값은 대부분 `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`

### 주의

- `ORDER BY` 절에서도 직접 사용 불가능. 단, **derived table 또는 CTE**로 wrapping 후 사용 가능

## Window Function Descriptions

### Ranking Functions

- `RANK()`: 동일 순위 존재 시 건너뜀 (e.g., 1, 1, 3)
- `DENSE_RANK()`: 동일 순위 존재해도 순서 유지 (e.g., 1, 1, 2)
- `ROW_NUMBER()`: 순서대로 고유한 번호 부여

### Aggregate Functions (with OVER)

- 기존 집계 함수들 (`SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`)도 `OVER()`와 함께 사용 가능
- `SUM(salary) OVER (PARTITION BY department)` → 부서별 총합

### Value Functions

- `FIRST_VALUE(expr)`: window 내 첫 번째 값
- `LAST_VALUE(expr)`: window 내 마지막 값
- `NTH_VALUE(expr, N)`: N번째 값

### Navigation Functions

- `LEAD(expr, offset)`: 현재 row 기준 **미래 row의 값**
- `LAG(expr, offset)`: 현재 row 기준 **이전 row의 값**

### CUME_DIST(), PERCENT_RANK()

- `CUME_DIST()`: 누적 분포
- `PERCENT_RANK()`: 상대적 순위 (0 ~ 1)

## Aggregate Functions

집계 함수는 **여러 row 값을 하나의 결과로 요약**할 때 사용.

### Aggregate Functions

| Function | Description |
| --- | --- |
| `AVG(expr)` | 평균 |
| `COUNT(expr)` / `COUNT(*)` | 개수 |
| `MAX(expr)` | 최대값 |
| `MIN(expr)` | 최소값 |
| `SUM(expr)` | 합계 |
| `GROUP_CONCAT(expr)` | 문자열로 합치기 (구분자 포함 가능) |

### DISTINCT 사용 가능

- `COUNT(DISTINCT column)`
- `SUM(DISTINCT column)`
- `AVG(DISTINCT column)`

중복을 제거한 상태로 계산함.

### GROUP_CONCAT Specifics

- 문자열을 하나로 합칠 때 사
    - `SEPARATOR`: 구분자 지정 (기본값은 `,`)
    - `ORDER BY` 사용 가능
    - `GROUP_CONCAT_MAX_LEN` 시스템 변수로 최대 길이 제한 조정 가능

```sql
sql
CopyEdit
SELECT GROUP_CONCAT(name ORDER BY name SEPARATOR '; ') FROM employees;
```

- NULL 값은 대부분 무시됨
- `HAVING` 절에서 집계 결과 필터링 가능
- **GROUP BY 없이도 전체 집합에 적용 가능**

## 📝 **문제 풀이**:

- 🔗 [LeetCode - Rank Scores](https://leetcode.com/problems/rank-scores/description/) `DENSE_RANK(`
    
    ```sql
    sql
    Copy
    SELECT score,
           DENSE_RANK() OVER (ORDER BY score DESC) AS rank
    FROM Scores;
    ```
    
- 🔗 [Solvesql - 다음날도 서울숲의 미세먼지 농도는 나쁨 😢](https://solvesql.com/problems/bad-finedust-measure/) `LEAD()`
    
    ```sql
    WITH cte AS (
      SELECT 
        DATE(measured_at) AS dt,
        pm10,
        LEAD(DATE(measured_at)) OVER (ORDER BY measured_at) AS next_day,
        LEAD(pm10) OVER (ORDER BY measured_at) AS next_pm10
      FROM measurements
    )
    SELECT 
      dt AS today,
      next_day,
      pm10,
      next_pm10
    FROM cte
    WHERE next_day = DATE_ADD(dt, INTERVAL 1 DAY)
      AND next_pm10 > pm10;
    ```
    
- 🔗 [programmers - 그룹별 조건에 맞는 식당 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131124)