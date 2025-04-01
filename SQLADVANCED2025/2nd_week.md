# 2nd_week

# 복합 JOIN

## 기본 JOIN 개요

- **JOIN**은 여러 테이블의 데이터를 **연결(combine)** 하여 하나의 결과 집합으로 반환하는 방식
- 보통 **공통된 컬럼 값**을 기준으로 테이블 간 데이터를 연결
- **JOIN 키워드 없이 쉼표(,)로 테이블을 나열**하는 것도 가능하지만, 명시적인 JOIN 문법이 더 권장

```sql
sql
CopyEdit
SELECT * FROM t1 JOIN t2 ON t1.id = t2.id;
```

---

## JOIN의 종류

### 1. **INNER JOIN** (또는 그냥 `JOIN`)

- 두 테이블에서 **조건을 만족하는 행만** 반환

```sql
sql
CopyEdit
SELECT * FROM t1 INNER JOIN t2 ON t1.id = t2.id;
```

---

### 2. **LEFT [OUTER] JOIN**

- 왼쪽 테이블(t1)의 **모든 행**과, 조건을 만족하는 오른쪽 테이블(t2)의 데이터를 반환
- 오른쪽에 일치하는 값이 없으면 `NULL` 반환

```sql
sql
CopyEdit
SELECT * FROM t1 LEFT JOIN t2 ON t1.id = t2.id;
```

### 3. **RIGHT [OUTER] JOIN**

- 오른쪽 테이블(t2)의 **모든 행**과, 조건을 만족하는 왼쪽 테이블(t1)의 데이터를 반환
- 왼쪽에 일치하는 값이 없으면 `NULL` 반환

```sql
sql
CopyEdit
SELECT * FROM t1 RIGHT JOIN t2 ON t1.id = t2.id;
```

---

### 4. **CROSS JOIN**

- **모든 조합**을 생성함 (카테시안 곱)
- 조건 없이 테이블을 곱셈함: `m` rows × `n` rows = `m*n` rows

```sql
sql
CopyEdit
SELECT * FROM t1 CROSS JOIN t2;
```

---

### 5. **STRAIGHT_JOIN**

- MySQL에게 조인 순서를 **명시적으로 지시**
- 옵티마이저가 순서를 바꾸지 않도록 강제

```sql
sql
CopyEdit
SELECT * FROM t1 STRAIGHT_JOIN t2 ON t1.id = t2.id;
```

## USING vs ON

- **USING(col)**: 공통된 컬럼 이름 하나일 때 간편하게 사용

```sql
sql
CopyEdit
SELECT * FROM t1 JOIN t2 USING (id);
```

- **ON t1.col = t2.col**: 더 일반적이며, 컬럼 이름이 다르거나 여러 조건이 필요한 경우 사용

```sql
sql
CopyEdit
SELECT * FROM t1 JOIN t2 ON t1.a = t2.b;
```

## NATURAL JOIN

- **공통된 컬럼 이름**이 자동으로 매칭되어 조인
- 자동화된 방식이라 **권장되지 않음** (명시적 ON/USING이 더 안전)

```sql
sql
CopyEdit
SELECT * FROM t1 NATURAL JOIN t2;
```

## 조인 시 주의사항

- **Ambiguous column names (모호한 컬럼명)**: 동일한 이름의 컬럼이 여러 테이블에 있으면 `t1.col`, `t2.col`처럼 **테이블 alias**를 써야 함.
- **NULL** 처리 주의: OUTER JOIN에서 연결이 안 된 테이블의 컬럼은 NULL로 채워짐.
- **조인 순서**와 인덱스는 성능에 큰 영향 있음.

## ORDER of Evaluation (평가 순서)

JOIN 문은 다음 순서로 처리됨:

1. `FROM` + `JOIN`
2. `WHERE`
3. `GROUP BY`
4. `HAVING`
5. `SELECT`
6. `ORDER BY`
7. `LIMIT`

---

# GROUP BY & HAVING

## GROUP BY

### 기본 개념

- **GROUP BY**는 결과를 하나 이상의 컬럼을 기준으로 그룹핑
- 보통 **집계 함수(Aggregate functions)** 와 함께 사용: `SUM()`, `COUNT()`, `AVG()`, `MIN()`, `MAX()` 등

### Syntax

```sql
sql
CopyEdit
SELECT group_column, aggregate_function
FROM table
GROUP BY group_column;
```

### 예제

```sql
sql
CopyEdit
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department;
```

- 부서별 직원 수를 계산.

### GROUP BY 없이도 Aggregate는 가능

```sql
sql
CopyEdit
SELECT AVG(salary) FROM employees;
```

- 전체 평균은 GROUP 없이 계산 가능.

### GROUP BY 다중 컬럼 가능

```sql
sql
CopyEdit
SELECT region, department, AVG(salary)
FROM employees
GROUP BY region, department;
```

- **지역 + 부서** 조합별 평균 급여를 계산.

### GROUP BY 컬럼과 SELECT

- GROUP BY에 포함되지 않은 컬럼을 SELECT에 넣을 경우,
    - **집계 함수로 감싸거나**,
    - **GROUP BY에 포함해야 함**

> (단, ONLY_FULL_GROUP_BY 모드에서는 이를 엄격히 제한함 – 이건 생략!)
> 

### 정렬과 함께 사용 가능

```sql
sql
CopyEdit
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department
ORDER BY num_employees DESC;
```

## SELECT 문 내 HAVING

- **GROUP BY로 그룹핑한 이후의 결과**에 대해 조건을 거는 절.
- **WHERE**과 달리, **집계 함수 결과를 필터링할 수 있음.**

### WHERE vs HAVING

| 절 | 언제 평가됨 | 집계 함수 사용 가능 여부 |
| --- | --- | --- |
| WHERE | GROUP BY 전에 | ❌ (집계 함수 사용 불가) |
| HAVING | GROUP BY 후에 | ✅ (집계 함수 사용 가능) |

### 예제 1 – 집계 함수 기준 필터링

```sql
sql
CopyEdit
SELECT department, COUNT(*) AS num_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 10;
```

- 직원이 10명 이상인 부서만 선택.

### 예제 2 – GROUP 없이도 사용 가능

```sql
sql
CopyEdit
SELECT AVG(salary) AS avg_salary
FROM employees
HAVING avg_salary > 50000;
```

- GROUP 없이도 HAVING은 사용할 수 있음 (집계 결과에 조건 적용).

### HAVING + ORDER BY

```sql
sql
CopyEdit
SELECT department, SUM(sales) AS total_sales
FROM employees
GROUP BY department
HAVING total_sales > 100000
ORDER BY total_sales DESC;
```

- HAVING은 결과 필터링 후, 정렬도 가능.

# 문제

## 문제1

```sql
SELECT 
    b.AUTHOR_ID,
    a.AUTHOR_NAME,
    b.CATEGORY,
    SUM(bs.SALES * b.PRICE) AS TOTAL_SALES
FROM BOOK b
JOIN BOOK_SALES bs
  ON b.BOOK_ID = bs.BOOK_ID
JOIN AUTHOR a
  ON b.AUTHOR_ID = a.AUTHOR_ID
WHERE bs.SALES_DATE >= '2022-01-01'
  AND bs.SALES_DATE < '2022-02-01'
GROUP BY b.AUTHOR_ID, a.AUTHOR_NAME, b.CATEGORY
ORDER BY b.AUTHOR_ID ASC, b.CATEGORY DESC;
```

## 문제2

```sql
SELECT
  CASE
    WHEN SUM(CASE WHEN s.CATEGORY = 'Front End' THEN 1 ELSE 0 END) > 0
         AND MAX(CASE WHEN s.NAME = 'Python' THEN 1 ELSE 0 END) = 1 THEN 'A'
    WHEN MAX(CASE WHEN s.NAME = 'C#' THEN 1 ELSE 0 END) = 1 THEN 'B'
    WHEN SUM(CASE WHEN s.CATEGORY = 'Front End' THEN 1 ELSE 0 END) > 0 THEN 'C'
    ELSE NULL
  END AS GRADE,
  d.ID,
  d.EMAIL
FROM DEVELOPERS d
JOIN SKILLCODES s ON (d.SKILL_CODE & s.CODE) > 0
GROUP BY d.ID, d.EMAIL
HAVING SUM(CASE WHEN s.CATEGORY = 'Front End' THEN 1 ELSE 0 END) > 0
    OR MAX(CASE WHEN s.NAME = 'C#' THEN 1 ELSE 0 END) = 1
ORDER BY GRADE ASC, d.ID ASC;
```