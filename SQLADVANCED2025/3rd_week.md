# 3rd_week

# CASE문 & 논리 연산자

MySQL에서 데이터를 다룰 때 조건에 따라 값을 처리하거나, 논리적으로 결과를 분기 처리하는 데 사용

## **CASE WHEN**

CASE 문은 SQL에서 조건에 따라 서로 다른 결과를 반환하도록 할 때 사용. 프로그래밍의 if-else 문과 유사한 역할

### 문법 구조

```sql
CASE
    WHEN 조건1 THEN 결과1
    WHEN 조건2 THEN 결과2
    ELSE 기본값
END
```

### CASE문의 두 가지 유형

### (1) **단순 CASE (Simple CASE)**

하나의 값을 여러 값과 직접 비교하여 결과를 반환

```sql
SELECT
    grade,
    CASE grade
        WHEN 'A' THEN 'Excellent'
        WHEN 'B' THEN 'Good'
        ELSE 'Average'
    END AS evaluation
FROM students;
```

### (2) **검색 CASE (Searched CASE)**

여러 개의 조건식을 평가하여 첫 번째로 참인 조건의 결과를 반환

```sql
SELECT
    price,
    CASE
        WHEN price < 100 THEN '저가'
        WHEN price BETWEEN 100 AND 500 THEN '중간가'
        ELSE '고가'
    END AS price_category
FROM products;
```

## **IF() 함수**

IF 함수는 조건이 참인지 거짓인지에 따라 두 가지 중 하나의 결과를 반환

### 문법 구조

```sql
IF(조건, 참일때 값, 거짓일때 값)
```

### 예시

매출이 1000 이상이면 'High', 미만이면 'Low'로 표시

```sql
SELECT
    revenue,
    IF(revenue >= 1000, 'High', 'Low') AS revenue_level
FROM sales
```

## **IFNULL() 함수**

IFNULL 함수는 첫 번째 인수가 NULL일 경우 두 번째 인수를 반환, NULL 처리에 유용

### 🔹 문법 구조

```sql
IFNULL(표현식, NULL일 때의 대체값)
```

### 🔹 예시

연락처가 없으면 '정보 없음' 표시

```sql
SELECT
    name,
    IFNULL(phone_number, '정보 없음') AS phone
FROM customer
```

## **NULLIF()**

두 값을 비교하여 서로 같다면 NULL을 반환하고, 다르면 첫 번째 값을 반환

### 문법 구조

```sql
NULLIF(표현식1, 표현식2)
```

### 예시

점수가 0이면 NULL로 처리

```sql
SELECT
    student_id,
    NULLIF(score, 0) AS valid_score
FROM test_results;
```

## **COALESCE()**

COALESCE 함수는 여러 인수 중 가장 먼저 등장하는 NULL이 아닌 값을 반환. 주로 여러 후보 중에서 사용 가능한 첫 번째 값을 가져올 때 사용

### 문법 구조

```sql
COALESCE(표현식1, 표현식2, 표현식3, ...)
```

### 예시

핸드폰 번호 → 집 전화번호 → '연락 불가' 순서로 값을 반환

```sql
SELECT
    customer_name,
    COALESCE(mobile, home_phone, '연락 불가') AS contact_info
FROM customer_contacts;
```

## **논리 연산자 (Logical Operators)**

SQL의 조건을 조합하거나 부정할 때 사용하는 연산자

### 주요 연산자

- **AND** : 양쪽 조건 모두 참이어야 참
- **OR** : 둘 중 하나의 조건이라도 참이면 참
- **NOT** : 조건을 반대로 바꿈 (참 → 거짓, 거짓 → 참)

### 예시

상태가 활성화이고 잔액이 1000 이상인 계좌만 선택

```sql
SELECT *
FROM accounts
WHERE status = 'active' AND balance >= 1000;
```

상태가 비활성화이거나 잔액이 부족한 계좌 선택

```sql
SELECT *
FROM accounts
WHERE status = 'inactive' OR balance < 0
```

특정 조건을 만족하지 않는 계좌 선택 (NOT 사용)

```sql
SELECT *
FROM accounts
WHERE NOT(status = 'closed');
```

- **CASE WHEN**과 **IF()** 함수는 조건에 따른 결과 처리를 직관적으로 수행할 때 유용
- **IFNULL(), NULLIF(), COALESCE()** 함수는 데이터 처리 과정에서 NULL을 효율적으로 처리하거나 제거할 때 필수적
- 논리 연산자 (**AND, OR, NOT**)는 복잡한 쿼리의 조건을 명확히 하고 원하는 데이터를 정확하게 추출하는 데 필수

---

# 문제

### 문제1

- 🔗 [HackerRank - 삼각형 종류 분류하기](https://www.hackerrank.com/challenges/what-type-of-triangle/problem) `CASE문`

```sql
SELECT
  CASE
    WHEN A + B <= C OR B + C <= A OR A + C <= B THEN 'Not A Triangle'
    WHEN A = B AND B = C THEN 'Equilateral'
    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
    ELSE 'Scalene'
  END AS triangle_type
FROM TRIANGLES;
```

### 문제2

- 🔗 [LeetCode - find-customer-referee](https://leetcode.com/problems/find-customer-referee/description/) `IS NULL`

```sql
SELECT name
FROM Customer
WHERE referee_id <> 2 OR referee_id IS NULL;
```