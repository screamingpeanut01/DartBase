# 4th_week

# GROUP_CONCAT

### 1. 함수 개요

`GROUP_CONCAT()` 함수는 그룹 내에서 문자열 값을 연결(concatenate)하여 하나의 문자열로 반환하는 **집계 함수**. `GROUP BY` 절과 함께 자주 사용

---

### 2. 기본 문법

```sql
GROUP_CONCAT([DISTINCT] expr [,expr ...]
             [ORDER BY {unsigned_integer | col_name | expr}
               [ASC | DESC] [,col_name ...]]
             [SEPARATOR str_val])

```

- **DISTINCT**: 중복된 값 제거함
- **expr**: 연결할 대상 열(또는 표현식)임
- **ORDER BY**: 연결 순서를 지정
- **SEPARATOR**: 구분자 설정 (기본값은 쉼표 `,`)

---

### 3. 예제

**테이블: employees**

| dept | name |
| --- | --- |
| HR | Alice |
| HR | Bob |
| Eng | Charlie |
| Eng | Dave |
| Eng | Emma |

```sql
SELECT dept, GROUP_CONCAT(name ORDER BY name SEPARATOR '; ') AS names
FROM employees
GROUP BY dept;
```

**결과:**

| dept | names |
| --- | --- |
| HR | Alice; Bob |
| Eng | Charlie; Dave; Emma |

---

### 4. 설정 변수

- `group_concat_max_len`: 반환 문자열의 최대 길이
    - 기본값은 1024
    - 세션/글로벌 단위로 조절 가능

```sql
SET SESSION group_concat_max_len = 10000;
```

---

### 5. 주의사항

- `GROUP_CONCAT()`은 결과가 `group_concat_max_len`을 초과하면 **잘림(truncated)** 현상이 발생
- `NULL` 값은 무시
- 순서가 중요할 경우 반드시 `ORDER BY`를 명시해야

---

### 6. 활용 예시

**(1) 여러 값 문자열로 묶기**

```sql
SELECT customer_id, GROUP_CONCAT(product_name)
FROM orders
GROUP BY customer_id;
```

**(2) 중복 제거**

```sql
SELECT customer_id, GROUP_CONCAT(DISTINCT product_name)
FROM orders
GROUP BY customer_id;
```

**(3) 동적 열 표현**

```sql
SELECT GROUP_CONCAT(DISTINCT CONCAT('SUM(CASE WHEN category = "', category, '" THEN sales END) AS ', category))
FROM sales;
```

---

### 7. 요약

| 항목 | 내용 |
| --- | --- |
| 기본 구분자 | `,` (쉼표) |
| 최대 길이 제한 | `group_concat_max_len` 변수로 설정 가능함 |
| NULL 처리 | NULL은 무시됨 |
| 중복 제거 | `DISTINCT` 키워드를 사용함 |
| 순서 지정 | `ORDER BY`를 사용함 |
| 커스터마이징 구분자 | `SEPARATOR` 키워드로 지정 가능함 |

`GROUP_CONCAT()`은 레코드를 문자열 하나로 요약하거나, 피벗 테이블 생성의 보조 수단으로 매우 유용

---

# **WITH RECURSIVE**

### 1. 개요

`WITH` 문은 **공통 테이블 표현식 (Common Table Expressions, CTE)**를 정의할 때 사용되며, `WITH RECURSIVE`는 **재귀적인 쿼리**를 작성할 수 있게 해줌. 복잡한 계층 구조나 반복적인 데이터 처리를 SQL만으로 수행 가능

---

### 2. 기본 문법

```sql
WITH RECURSIVE cte_name (col1, col2, ...) AS (
    initial_query
    UNION [ALL]
    recursive_query
)
SELECT ... FROM cte_name;

```

- `initial_query`: 재귀의 시작점 (anchor member)
- `recursive_query`: 재귀 반복 쿼리 (recursive member)
- `UNION [ALL]`: 결과를 합침. 중복 허용 시 `UNION ALL`을 사용

---

### 3. 예제: 계층 구조 탐색

**테이블: employees**

| id | name | manager_id |
| --- | --- | --- |
| 1 | CEO | NULL |
| 2 | VP | 1 |
| 3 | Lead | 2 |
| 4 | Dev | 3 |

```sql
WITH RECURSIVE hierarchy AS (
  SELECT id, name, manager_id, 1 AS level
  FROM employees
  WHERE manager_id IS NULL

  UNION ALL

  SELECT e.id, e.name, e.manager_id, h.level + 1
  FROM employees e
  JOIN hierarchy h ON e.manager_id = h.id
)
SELECT * FROM hierarchy;
```

**결과:**

| id | name | manager_id | level |
| --- | --- | --- | --- |
| 1 | CEO | NULL | 1 |
| 2 | VP | 1 | 2 |
| 3 | Lead | 2 | 3 |
| 4 | Dev | 3 | 4 |

---

### 4. 활용

- 트리 구조 탐색 (조직도, 카테고리, 댓글 등)에 사용
- 경로 추적, 순환 계산에 활용
- 재귀적 합계 또는 순위 계산에 유용

---

### 5. 주의사항

- 반드시 anchor 쿼리와 recursive 쿼리를 `UNION [ALL]`로 결합해야
- 무한 루프 방지를 위해 종료 조건이 필수 (ex. `WHERE` 또는 `LIMIT`)
- `max_execution_time`이 작을 경우 실행 제한에 걸릴 수 있음

---

### 6. 요약

| 항목 | 내용 |
| --- | --- |
| 핵심 키워드 | `WITH RECURSIVE`, `UNION ALL`을 사용 |
| anchor 쿼리 | 초기 결과를 생성 |
| recursive 쿼리 | 이전 결과에 기반하여 반복 확장 |
| 활용 예시 | 조직도, 카테고리 트리, 댓글 스레드 등에 사용 |
| 주의 사항 | 종료 조건 없으면 무한 루프 위험이 존재 |

`WITH RECURSIVE`는 복잡한 계층 데이터를 정규 SQL로 처리할 수 있게 해주는 기능

# 문제

## 문제1

🔗 [programmers - 우유와 요거트가 담긴 장바구니](https://school.programmers.co.kr/learn/courses/30/lessons/62284) **`GROUP_CONCAT()`**

```sql
WITH CART_ITEM_LIST AS (
    SELECT
        CART_ID,
        GROUP_CONCAT(DISTINCT NAME ORDER BY NAME) AS ITEMS
    FROM
        CART_PRODUCTS
    GROUP BY
        CART_ID
)
SELECT
    CART_ID
FROM
    CART_ITEM_LIST
WHERE
    ITEMS LIKE '%Milk%'
    AND ITEMS LIKE '%Yogurt%'
ORDER BY
    CART_ID
```

## 문제2

🔗 [programmers - 입양 시각 구하기(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59413) **`WITH RECURSIVE`**

```sql
WITH RECURSIVE hours AS (
    SELECT 0 AS HOUR
  UNION ALL
    SELECT HOUR + 1
    FROM hours
    WHERE HOUR < 23
)
SELECT
    h.HOUR                       AS HOUR,
    COALESCE(COUNT(a.ANIMAL_ID), 0) AS COUNT
FROM
    hours AS h
    LEFT JOIN ANIMAL_OUTS AS a
      ON h.HOUR = HOUR(a.DATETIME)
GROUP BY
    h.HOUR
ORDER BY
    h.HOUR;
```