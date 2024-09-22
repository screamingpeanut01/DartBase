# INTRO

0802 - 0805 tableau study

강의 28 ~ 37강 수강

강의 내용에 해당하는 5문제 제작

데이터셋 선정 및 실습


<br>

# 데이터셋 설명

사용할 데이터는 'superstore.csv' 데이터셋이다.
superstore dataset의 구성은 다음과 같다.

| Column Name       | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| Order ID          | Unique identifier for each order                                            |
| Order Date        | Date when the order was placed                                              |
| Ship Date         | Date when the order was shipped                                             |
| Ship Mode         | Shipping method used for the order                                          |
| Customer ID       | Unique identifier for each customer                                         |
| Customer Name     | Name of the customer                                                        |
| Segment           | Segment to which the customer belongs                                       |
| Country           | Country where the customer is located                                       |
| City              | City where the customer is located                                          |
| State             | State where the customer is located                                         |
| Postal Code       | Postal code of the customer                                                 |
| Region            | Region where the customer is located                                        |
| Product ID        | Unique identifier for each product                                          |
| Category          | Category of the product                                                     |
| Sub-Category      | Sub-category of the product                                                 |
| Product Name      | Name of the product                                                         |
| Sales             | Sales amount for the order                                                  |
| Quantity          | Quantity of the product ordered                                             |
| Discount          | Discount applied to the order                                               |
| Profit            | Profit generated from the order                                             |
| Shipping Cost     | Cost of shipping for the order                                              |
| Order Priority    | Priority level of the order                                                 |

<br>

<br>

# 강의 정리

## 28강. 필터

<!-- 필터 강의를 듣고 알게 된 점에 대해 미래의 내게 도움이 되도록 정리해주세요.  -->
<!-- 이미지는 캡쳐 후 Copy Path로 저장 경로를 포함해주세요.-->
<!-- ```js {글자} ``` 안에 글자를 넣게 되면 코드스니펫 안에 표시되게 됩니다.-->
<br> 

> 추출, 데이터원본, 컨텍스트, 차원, 측정값, 필터 순으로 동작함.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-2.png?raw=true)

(라이브X) 데이터를 추출해서 필터링을 적용하면 필터링된 상태의 새 데이터셋이 저장되며,

로컬 데이터와 연동하여 작업하게 됨.

데이터 원본 필터는 작업을 위한 데이터 중 일부만 워크스페이스에 불러오는 경우 사용 

> 컨텍스트 필터

모든 행에 엑세스하도록 적용되며,
다른 필터가 컨텍스트 필터에 종속됨.

ex. 제품의 필터 두 개가 독립적으로 작용하는 경우 어떻게 해결해야 할까? -> 컨텍스트 필터 사용하여 데이터셋의 원본을 먼저 제한
기본 필터는 노출되는 행만 제한하지, 계산 결과를 제한하지는 못함.

필드 색상이 회색으로, 가장 상위에 위치됨.
컨텍스트 필터 먼저 사용하면 쿼리 속도가 향상

> 차원 필터
(측정값에 제한을 두고 싶다고 할 때, 어떤 기준으로 그룹화하여 필터링할 것인지에 관함)


### 문제1
```js
유정이는 superstore 데이터셋에서 '주문' 테이블을 보고 있습니다.
1) 국가/지역 - 시/도- 도시 의 계층을 생성했습니다. 계층 이름은 '위치'로 설정하겠습니다.
2) 날짜의 데이터 타입을 '날짜'로 바꾸었습니다.

코로나 시기의 도시별 매출 top10을 확인하고자
1) 배송 날짜가 코로나시기인 2021년, 2022년에 해당하는 데이터를 필터링했고
2) 위치 계층을 행으로 설정해 펼쳐두었습니다.
이때, 수익의 합계가 TOP 10인 도시들만을 보았습니다.
```

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-4.png?raw=true)

```
겉보기에는 전체 10개로, 잘 나온 결과처럼 보입니다. 그러나 유정이는 치명적인 실수를 저질렀습니다.
오늘 배운 '컨텍스트 필터'의 내용을 고려하여 올바른 풀이 및 결과를 구해주세요.
```

### 풀이 결과

<img width="592" alt="스크린샷 2024-08-05 오전 9 22 20" src="https://github.com/user-attachments/assets/63b66490-cbe9-420d-bf05-8dd6cb8848af">

```
유정이는 필터 두 개를 독립적으로 설정했으므로 문제가 발생하였습니다.
배송 날짜 필터가 컨텍스트 필터로 설정되지 않았기 때문에, 수익의 합계 TOP 10 도시를 필터링할 때 전체 데이터셋이 사용됩니다.
즉, 2016년부터 2024년까지의 모든 데이터를 포함하여 수익의 상위 10개 도시를 계산하게 됩니다.

전체 기간 동안의 상위 10개 도시가 필터링되므로, 코로나 시기(2021년, 2022년)의 데이터가 반영되지 않습니다. 이는 코로나 시기의 데이터를 기준으로 한 것이 아닙니다.

컨텍스트 필터는 데이터 필터링의 맥락을 제공하여, 다른 필터가 작용하기 전에 먼저 적용되게 합니다. 컨텍스트 필터가 없다면 다른 필터들이 적용될 때 전체 데이터셋의 기준이 됩니다.
```

<br>

## 29강. 그룹

그룹, 계층, 집합

>그룹을 만드는 법

뷰에서 드래그로 그룹을 묶을 수도 있지만, 그룹을 만들고자 하는 필드에서 만들기 -> 그룹을 눌러도 같음.
기타포함을 만들 수 있음.
그룹에서 해제하게 되면 뷰에서도 노출되지 않음.

## 30강. 계층

계층은 뷰에서 데이터를 drill down해 값을 세부적으로 찾을 때 유용함.
날짜나, category-subcategory-product 식으로 포함 관계에 있는 경우 유용
지역 - 국가 - 시/도 - 도시로 묶을 수도 있음.

## 31강. 집합

집합은 사용자가 어떤 조건을 설정하고, 조건을 기반으로 데이터를 분류하는 방법임.
수익을 많이 낸 상위 10개를 구분하기 위해서도 집합을 표현 가능
> 일반, 조건, 상위 세 종류로 구성

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-11.png?raw=true)


이때, '세그먼트 기준 매출 10위'라고 한다면 매출 측정값에서 집합을 만드는 것이 아니라 세그먼트에서 만들어야 함.

작성하면 데이터 패널에 필드가 생성되어, 필터 혹은 색상 등 마크에 적용할 수도 있음.
데이터가 업데이트 되어도 유동적으로 반응함.

## 32강. 결합집합

집합을 활용하여 지정 조건에 따라 데이터를 구분할 수 있음. \
두 가지 조건을 적용할 때 결합된 집합을 사용함.\
*두 가지 조건에 동시 해당하는 집합을 찾고자 할 때 결합집합을 이용*

<br>
- 결합집합을 만들 수 있는 방법은?

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image.png?raw=true)

합집합, 교집합, 하나에만 속하는 집합을 선택할 수 있음.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image.png?raw=true)

측정값 -> 기본 속성 -> 숫자 형식
백분률을 확인하고자 하는 형식으로 평가할 수 있음.

집합의 결과와 동일하게 IN/OUT으로 표시됨.


<br>

## 33. 계산된 필드

태블로에는 행 수준 계산과 집계 계산이 있음
행 수준으로 계산되어 값이 정확하지 않음
필드 옆에 =# 처럼 등호가 생긴 경우 계산된 필드라는 의미
기본 숫자 형식을 표시하는 방법을 지정할 수 있음


### 문제 2


```js

지금 데이터셋의 측정값에는 매출, 수량, 수익, 할인율이 있습니다. 경영 시각화에 추가로 많이 사용되는 변수를 몇 개 더 만들어보겠습니다.

1) 연간 매출 성장률(Year-over-Year Growth)를 만들어주세요.

Hint: 매출 - 작년 매출 / 작년 매출(절댓값) 입니다. LOOKUP 함수를 사용해주세요.

2) 주문당 평균 이익(Average Profit per Order)를 만들어주세요.

3) 총 매출 대비 이익률 (Profit Margin)을 만들어주세요.

4) 배송 지연일(Delivery Delay Days)을 만들어주세요.

5) 또 필요하다고 생각되는 다른 매개변수를 구상해보세요.
``` 

### 문제 풀이

 계산된 필드를 만들 때, 행 단위로 만들 것인지 혹은 뷰에서 그때그때 Groupby 기준에 따라 달라지는 집계 함수로 만들 것인지를 구분하는 것이 필요합니다.


1) 연간 매출 성장률
> (SUM([Sales]) - LOOKUP(SUM([Sales]), -1)) / ABS(LOOKUP(SUM([Sales]), -1))

작년 Sales의 값을 LOOKUP 함수를 사용하여 찾습니다.
이 경우, 각각 Row에서 매출 성장률을 구하는 것이 아니라 차원을 기준으로(이 경우 YEAR이 차원이 됩니다) Sales를 합한 뒤 계산하기 때문에, 행 단위가 아닌 집계 계산을 수행하게 됩니다.


2) 주문당 평균 이익
> SUM([Profit]) / COUNTD([Order ID])

주문당 평균 이익을 구할 때, 전체 Profit에 주문 건수를 나누면 평균을 구할 수 있겠네요.

3) 총 매출 대비 이익률
> SUM([Profit]) / SUM([Sales])

4) 배송 지연일
> DATEDIFF('day', [Order Date], [Ship Date])


<br>

## 34. 행수준계산

> 행수준계산에는 기본 계산, 테이블 계산, LOD 표현식이 있다.

행수준계산은 각 레코드를 통해 계산, 집계 계산은 현재 보이는 뷰를 기준으로 계산하는 것.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-12.png?raw=true)

IF ~ THEN 문법에 익숙해지기

### 문제 3

```js

가장 많이 주문한 사람들은 물건 배송을 빨리 받았을까요?
1) 국가/지역별(이하 '나라'로 통칭), 범주별로 배송일자가 다를 수 있으니 먼저, 나라별/범주별로 평균 배송일자를 설정한 뒤, 
2) 각 나라에서 가장 많이 주문한 사람의 이름을 첫 번째 열, 
3) 그 사람이 주문한 제품 이름을 2번째 열, 
4) 각 상품이 배송까지 걸린 날 수를 표현하고
5) 그리고 만약 배송이 각 나라/범주별 평균보다 빨랐다면 '빠름', 같다면 '평균', 느리다면 '느림' 으로 print 해주세요.

``` 
![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-19.png?raw=true)
### 풀이 과정

먼저, 계산된 필드 만들기를 이용하여 식을 계산합니다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-7.png?raw=true)

> DATEDIFF('day', [배송 날짜], [주문 날짜])

이때, 집계함수가 아니라 각 row 자체에서 배송에 걸린 기간을 계산하고 싶으므로 단순 계산식으로 표현해야 합니다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-9.png?raw=true)

배송까지 걸린 일수를 계산하는 것은 집계에 따라, 혹은 레코드에 따라 다른 것이 아니라 전체 데이터셋에서 국가/지역 및 범주 별로 사전에 계산되어야 하는 상수이므로, FIXED(LOD)로 계산을 해 둔다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-10.png?raw=true)

국가/지역, 고객ID 별로 주문ID의 개수를 세어 둡니다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-16.png?raw=true)

그래서 가장 많은 주문 수량을 정해둡니다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-17.png?raw=true)
그래서 그것과 같은 값의, 가장 많이 주문한 고객을 FIX해둡니다.
FIXED 된 것들은 뷰에 따라 바뀌어서는 안됩니다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-18.png?raw=true)

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-19.png?raw=true)
결과는 이렇게 나옵니다.

### 문제 4

```
![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-13.png?raw=true)
주문ID별로 주문 처리에 걸리는 시간(DATEDIFF 함수를 사용하여 주문 날짜와 배송 날짜의 차를 구함)을 표시하였습니다.

이때, 2번째 행에서는 11월 26일 ~ 11월 30일까지 4일이 걸렸음에도 불구, 주문 처리일은 12일로 뜹니다.
왜 이런 일이 발생하는 것이며, 이 경우 어떻게 처리할 수 있을까요?

```

### 문제풀이


```
위 경우는 한 Order ID에 대하여 여러 Product가 속해 있을 것으로 추정됩니다. 
즉, Order ID는 하나이지만 이에 대해 여러 개의 ROW들이 속해 있는 상태인 것입니다.
지금 측정값이 자연스레 '합계(SUM)'으로 마크에 표시되어 있습니다.
이를 AVG로 바꾸어주거나 측정값에서 차원으로 변경하여 해결할 수 있습니다.

```

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-14.png?raw=true)


<br>


## 35. 집계계산

현재 뷰에서 보이는 기준으로 집계하는 것
표시된 계산 함수를 변경할 수도 있음.



- 태블로 집계 함수의 종류

                                            
| 집계 함수       | 설명                                                                                  |
|-----------------|---------------------------------------------------------------------------------------|
| SUM()           | 지정된 숫자 표현식의 합계를 반환합니다.                                                |
| AVG()           | 지정된 숫자 표현식의 평균을 반환합니다.                                                |
| MIN()           | 지정된 숫자 표현식의 최소값을 반환합니다.                                              |
| MAX()           | 지정된 숫자 표현식의 최대값을 반환합니다.                                              |
| COUNT()         | 지정된 표현식의 비어 있지 않은 항목 수를 반환합니다.                                    |
| COUNTD()        | 지정된 표현식의 고유 항목 수를 반환합니다.                                              |
| MEDIAN()        | 지정된 숫자 표현식의 중앙값을 반환합니다.                                               |
| STDEV()         | 모집단의 표준 편차를 반환합니다.                                                        |
| STDEVP()        | 표본의 표준 편차를 반환합니다.                                                        |
| VAR()           | 모집단의 분산을 반환합니다.                                                           |
| VARP()          | 표본의 분산을 반환합니다.                                                            |
| ATTR()          | 지정된 표현식이 모든 행에 대해 동일한 값을 가지면 해당 값을 반환하고, 그렇지 않으면 `*`을 반환합니다. |
| ZN()            | 지정된 표현식이 null이면 0을 반환하고, 그렇지 않으면 표현식 값을 반환합니다.          |
| PERCENTILE()    | 지정된 백분위수에 해당하는 값을 반환합니다.                                           |
| RAWSQLAGG()     | 사용자 정의 집계 함수를 SQL로 직접 실행할 수 있습니다.                                |
| WINDOW_SUM()    | 창의 모든 값을 합산합니다.                                                            |
| WINDOW_AVG()    | 창의 모든 값의 평균을 계산합니다.                                                      |
| WINDOW_MIN()    | 창의 모든 값의 최소값을 반환합니다.                                                    |
| WINDOW_MAX()    | 창의 모든 값의 최대값을 반환합니다.                                                    |
| WINDOW_COUNT()  | 창의 모든 값을 셉니다.                                                                |
| WINDOW_MEDIAN() | 창의 모든 값의 중앙값을 반환합니다.                                                   |
| WINDOW_VAR()    | 창의 모든 값의 분산을 반환합니다.                                                     |
| WINDOW_STDEV()  | 창의 모든 값의 표준 편차를 반환합니다.                                                |
| WINDOW_PERCENTILE() | 창의 값들에서 지정된 백분위수에 해당하는 값을 반환합니다.                        |
| TOTAL()         | 전체 테이블 또는 창의 값을 합산합니다.                                                |
| CORR()          | 두 표현식 간의 피어슨 상관 계수를 반환합니다.                                          |
| COVAR()         | 모집단 공분산을 반환합니다.                                                           |
| COVARP()        | 표본 공분산을 반환합니다.                                                            |
| SIZE()          | 현재 창의 크기(행 수)를 반환합니다.                                                   |
| INDEX()         | 현재 행의 인덱스를 반환합니다.                                                        |
| FIRST()         | 창의 첫 번째 행부터 현재 행까지의 오프셋을 반환합니다.                                |
| LAST()          | 창의 마지막 행부터 현재 행까지의 오프셋을 반환합니다.                                |
| RANK()          | 창의 값에 대한 순위를 반환합니다.                                                     |
| RANK_DENSE()    | 창의 값에 대한 밀집 순위를 반환합니다.                                               |
| RANK_MODIFIED() | 창의 값에 대한 수정된 순위를 반환합니다.                                             |
| RANK_UNIQUE()   | 창의 값에 대한 고유 순위를 반환합니다.                                               |
| RUNNING_SUM()   | 현재 행까지의 누적 합계를 반환합니다.                                                 |
| RUNNING_AVG()   | 현재 행까지의 누적 평균을 반환합니다.                                                 |
| RUNNING_MIN()   | 현재 행까지의 누적 최소값을 반환합니다.                                               |
| RUNNING_MAX()   | 현재 행까지의 누적 최대값을 반환합니다.                                               |
| RUNNING_COUNT() | 현재 행까지의 누적 개수를 반환합니다.                                                 |

| LOD 표현식 함수 | 설명                                                                                  |
|-----------------|---------------------------------------------------------------------------------------|
| FIXED           | 지정된 차원 수준에서 집계를 고정합니다. 이 표현식은 주어진 차원에서 데이터를 집계한 다음, 결과를 반환합니다. |
| INCLUDE         | 시트에 표시된 차원뿐만 아니라 추가적으로 지정된 차원에 대해서도 집계를 포함합니다. 즉, 현재 시트에서 사용된 차원 외에 지정한 차원도 고려하여 집계합니다. |
| EXCLUDE         | 시트에서 사용된 차원 중에서 특정 차원을 제외하고 집계합니다. 즉, 현재 시트에서 사용된 차원 중에서 지정한 차원을 제외하고 집계합니다. |

<br>

집계로 표시된 것과 합계로 표시된 것의 차이
집계는 계산 수단을 변경할 수 없음.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-20.png?raw=true)

하나의 주문에 여러 상품이 포함되는 경우, 상품별로 ROW가 나뉘므로
주문 당으로 계산하고자 하는 경우에는 COUNTD 함수로 INDEX를 만들어 사용한다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-21.png?raw=true)

따라서, 년도별 주문건수를 확인하고 싶을 때 Quantity 특성을 살리는 것이 아니라 주문 행위 그 자체의 숫자를 세고 싶다면, 반드시 고유 주문건수라는 새로운 필드를 만들어 사용해야 한다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-22.png?raw=true)

실제로 하나의 주문ID에 대해 중복되던 데이터들이 많았다.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-23.png?raw=true)

이것은 고유 주문번호를 달지 않은 채 표현한 것.
수에서 확연한 차이가 난다.

## 36. 테이블 계산

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-24.png?raw=true)

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-25.png?raw=true)

생성된 필드의 세모표시는 테이블 계산 필드의 의미

확인해보면, 지금 옆으로 합산하도록 누계가 표시되고 있음.
BUT 우리는 년도별 집계를 원하는 것

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-26.png?raw=true)

따라서 테이블(아래에서 옆으로)로 누계합산을 표현할 수 있음.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-27.png?raw=true)

참고로 '특정 차원'을 이용하면 누적하고자 하는 범위를 선택할 수 있음.

![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-29.png?raw=true)
![image-2.png](https://github.com/yousrchive/tableau/blob/main/study/img/1st%20study/image-28.png?raw=true)

전년대비 매출 증감 표현



### 37. 퀵테이블계산(1) 

> 1) 누계

집계한 값을 누적한 값으로 한번 더 계산하는 것

![스크린샷](../study/img/2nd%20study/스크린샷%202024-08-12%20오전%201.14.01.png)

세모 표시가 나타난다는 건 테이블 계산이 포함되었음을 의미

> 2) 차이

측정값이 기준값과 얼마나 차이나는지를 계산

✅ '기준' 옵션에는 **이전, 다음, 첫 번째, 지난** 총 4가지가 있음

측정값이 기준값과 어느 정도 떨어져 있는지를 확인할 수 있음

> 3) 비율 차이: 측정값들 사이에 성장률 차이

![스크린샷](../study/img/2nd%20study/스크린샷%202024-08-12%20오전%201.18.17.png)

✅ 비율 차이

차트에 0을 기준으로 지난 달에 비해 이번 달에 얼마나 수익을 냈는 지 확인할 수 있음!

지역별 제품 매출 순위


![스크린샷](../study/img/2nd%20study/스크린샷%202024-08-12%20오전%201.21.17.png)

퀵 테이블 계산에서 순위 선택
전체 순위가 아니라, 해당 지역별로 순위가 보고 싶은 경우 추가 설정

✅ 다음을 사용하여 계산

> 4) 백분위수

전체에서 각 멤버들의 백분위수를 표시하도록 함

매출 최대가 100%, 최저가 0%로 표시됨

