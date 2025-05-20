# 6th_week

### **1️⃣ 과제 안내**

 지금까지 학습한 SQL 개념들을 **종합적으로 활용**하여 문제를 해결해보세요!

 0~5주차 과제에서는 주차별로 명확한 학습 주제를 제시하고, 해당 개념을 적용하는 방식으로 쿼리 작성 연습을 진행하였다면, 이번 6주차 과제에서는 별도의 주제나 개념을 제시하지 않고, 오직 문제만을 바탕으로 쿼리를 설계하고 작성해야 합니다.

 이번 과제에서는 문제를 이해하고 필요한 지표와 분석 방향을 스스로 판단하여 쿼리를 구성하는 사고력을 기르는 것을 목표로 합니다.

 아래의 항목을 사전에 정리한 뒤 쿼리를 작성하면 문제 해결에 필요한 흐름을 구조화하는 데 도움이 될 수 있습니다.

```jsx
**[쿼리 작성 템플릿]**
- 쿼리를 작성하는 목표, 확인할 지표:
- 쿼리 계산 방법:
- 데이터의 기간:
- 사용할 테이블:
- Join KEY:
- 데이터 특징:
```

📝 **문제 풀이**: 

- 🔗 [solvesql - 복수 국적 메달 수상한 선수 찾기](https://solvesql.com/problems/multiple-medalist/)
    - **목표/지표:** 여러 종목 메달리스트 이름 찾기.
    - **계산 방법:** 선수별 서로 다른 종목 수 계산 후, 1 초과 선수 필터링.
    - **데이터 기간:** `Medalists` 테이블 전체.
    - **사용 테이블:** `Medalists`.
    - **Join KEY:** 없음 (단일 테이블 집계).
    - **데이터 특징:** `Medalists` 테이블 (`name`, `discipline` 컬럼). 동일 종목 중복 메달은 1개 종목으로 취급.
    
    ```sql
    SELECT
      name
    FROM Medalists
    GROUP BY
      name
    HAVING
      COUNT(DISTINCT discipline) > 1;
    ```
    
- 🔗 [solvesql - 온라인 쇼핑몰의 월 별 매출액 집계](https://solvesql.com/problems/shoppingmall-monthly-summary/)
    - **목표/지표:** 쇼핑몰 월별 요약 (구매 유저 수, 주문 수, 매출액).
    - **계산 방법:**
        - 월별로 그룹화.
        - 구매 유저 수: `COUNT(DISTINCT user_id)`.
        - 주문 수: `COUNT(id)`.
        - 매출액: `SUM(total_price)`.
    - **데이터 기간:** `orders` 테이블 전체
    - **사용 테이블:** `orders`.
    - **Join KEY:** 없음
    - **데이터 특징:**
        - `orders` 테이블 (`id` AS order_id, `created_at` AS order_timestamp, `user_id`, `total_price`).
        - `created_at` 필드를 사용하여 연도와 월 추출.
    
    ```sql
    SELECT
      STRFTIME('%Y', created_at) AS year,
      STRFTIME('%m', created_at) AS month,
      COUNT(DISTINCT user_id) AS purchasing_users,
      COUNT(id) AS orders,
      SUM(total_price) AS revenue
    FROM
      orders
    GROUP BY
      year,
      month
    ORDER BY
      year ASC,
      month ASC;
    ```
    
- 🔗 [solvesql - 세 명이 서로 친구인 관계 찾기](https://solvesql.com/problems/friend-group-of-3/)
    - **목표/지표:** 세 사람이 서로 모두 친구인 관계(삼각 친구 관계)의 총 그룹 수 계산.
    - **계산 방법:**
        - `Friends` 테이블을 3번 JOIN하여 `A-B`, `B-C`, `C-A` 관계를 만족하는 세 사람 (`A`, `B`, `C`)
        - `A`, `B`, `C`는 `f1.person1`, `f1.person2`, `f2.person2`로 각각 지정
        - `A < B < C` 조건을 적용하여 각 그룹이 한 번만 계산
        - 최종적으로 조건을 만족하는 그룹 수를 `COUNT(*)`
    - **데이터 기간:** `Friends` 테이블 전체 데이터.
    - **사용 테이블:** `Friends` (별칭 `f1`, `f2`, `f3` 사용).
    - **Join KEY:**
        - `f1` (A-B): `f1.person1` (A), `f1.person2` (B)
        - `f2` (B-C): `f1.person2 = f2.person1` (B로 연결), `f2.person2` (C)
        - `f3` (C-A): `f2.person2 = f3.person1` (C로 연결), `f1.person1 = f3.person2` (A로 연결)
    - **데이터 특징:**
        - `Friends` 테이블은 `person1`, `person2` 컬럼으로 구성, 두 사람의 친구 관계
        - 쿼리는 `(A,B)`, `(B,C)`, `(C,A)` 순서의 친구 관계가 테이블에 명시적으로 존재해야

---