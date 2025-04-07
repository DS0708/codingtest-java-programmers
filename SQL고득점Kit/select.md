# SQL 고득점 kit - SELECT

<br>

## 흉부외과 또는 일반외과 의사 목록 출력하기
- 문제
```
DOCTOR 테이블에서 진료과가 흉부외과(CS)이거나 일반외과(GS)인 의사의 이름, 의사ID, 진료과, 고용일자를 조회하는 SQL문을 작성해주세요. 
이때 결과는 고용일자를 기준으로 내림차순 정렬하고, 고용일자가 같다면 이름을 기준으로 오름차순 정렬해주세요.
```
- SQL
```sql
SELECT DR_NAME, DR_ID, MCDP_CD, date_format(HIRE_YMD, '%Y-%m-%d') as HIRE_YMD
    from DOCTOR
    where MCDP_CD = 'CS' or MCDP_CD = 'GS'
    ORDER BY HIRE_YMD DESC, DR_NAME;
```
### SQL의 date_format()
SQL의 DATE 타입은 YYYY-MM-DD hh:mm:ss 형식이다.
따라서 원하는 형식으로 출력하기 위해서는 date_format()이 필요함.
#### 날짜 및 요일
| 포맷 형식 | 결과값   |
|-----------|----------|
| `%Y`      | 2025     |
| `%y`      | 25       |
| `%M`      | February |
| `%b`      | Feb      |
| `%m`      | 02       |
| `%d`      | 01       |
| `%e`      | 1        |
| `%a`      | Thu      |
#### 시간
| 포맷 형식 | 결과값      |
|-----------|-------------|
| `%H`      | 18 (24시간) |
| `%h`      | 6 (12시간)  |
| `%i`      | 31 (분)     |
| `%s` / `%S` | 45 (초)   |
| `%m`      | 02          |



## 과일로 만든 아이스크림 고르기
- 문제
```
상반기 아이스크림 총주문량이 3,000보다 높으면서 아이스크림의 주 성분이 과일인 아이스크림의 맛을 총주문량이 큰 순서대로 조회하는 SQL 문을 작성해주세요.
```
- SQL
```sql
SELECT ICECREAM_INFO.FLAVOR from FIRST_HALF join ICECREAM_INFO on FIRST_HALF.FLAVOR = ICECREAM_INFO.FLAVOR
WHERE FIRST_HALF.TOTAL_ORDER > 3000 and ICECREAM_INFO.INGREDIENT_TYPE = 'fruit_based'
ORDER BY FIRST_HALF.TOTAL_ORDER DESC;
```

<br>
<br>
<br>

## 평균 일일 대여 요금 구하기
- 문제
```
CAR_RENTAL_COMPANY_CAR 테이블에서 자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요. 
이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고, 컬럼명은 AVERAGE_FEE 로 지정해주세요.
```
- SQL
```sql
SELECT ROUND(AVG(DAILY_FEE),0) as AVERAGE_FEE 
    from CAR_RENTAL_COMPANY_CAR
    where CAR_TYPE='SUV';
```
### SQL의 ROUND
ROUND 함수는 SQL에서 숫자를 소수점 특정 자리에서 반올림하는데 사용되며, 두 개의 인자를 받음.

- 첫 번째 인자: 반올림하고자 하는 열(Column)이나 수식(Expression)
- 두 번째 인자: 반올림할 소수점 자리를 지정. 이 값이 양수면 지정된 자리수까지 소수점 아래를 반올림합니다. 음수일 경우 정수 부분의 특정 자리에서 반올림(예: -1은 십의 자리에서 반올림).

예를 들어, ROUND(123.4567, 2)는 123.46을 반환하고, ROUND(123.4567, 0)는 123을 반환한다. 또한, ROUND(123.4567, -1)는 120을 반환하여 십의 자리에서 반올림한다.


<br>
<br>
<br>

## 강원도에 위치한 생산공장 목록 출력하기
- 문제
```
FOOD_FACTORY 테이블에서 강원도에 위치한 식품공장의 공장 ID, 공장 이름, 주소를 조회하는 SQL문을 작성해주세요. 이때 결과는 공장 ID를 기준으로 오름차순 정렬해주세요.
```
- SQL
```sql
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
    FROM FOOD_FACTORY
    WHERE ADDRESS LIKE '강원도%';
```

### LIKE
- % 기호
이 기호는 0개 이상의 임의의 문자를 대체.
예를 들어 LIKE '강원도%'는 "강원도"로 시작하는 모든 문자열을 찾는다.
따라서 "강원도 춘천시", "강원도 원주시" 등이 해당된다.

- _ 기호
이 기호는 정확히 하나의 임의의 문자를 대체.
예를 들어 LIKE '010-____-____'는 "010-" 다음에 정확히 8개의 문자가 오는 문자열을 찾는다.


<br>
<br>
<br>

## 12세 이하인 여자 환자 목록 출력하기
- 문제
```
PATIENT 테이블에서 12세 이하인 여자환자의 환자이름, 환자번호, 성별코드, 나이, 전화번호를 조회하는 SQL문을 작성해주세요. 이때 전화번호가 없는 경우, 'NONE'으로 출력시켜 주시고 결과는 나이를 기준으로 내림차순 정렬하고, 나이 같다면 환자이름을 기준으로 오름차순 정렬해주세요.
```
- SQL
```sql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, COALESCE(TLNO, 'NONE') AS TLNO
    FROM PATIENT
    WHERE AGE <= 12 AND GEND_CD = 'W'
    ORDER BY AGE DESC, PT_NAME;
```

### COALESCE
병합한다는 의미의 coalesce 함수로,
조건에 따라서 두 칼럼을 합치는 기능을 한다.

```sql
SELECT A, B, COALESCE(A, B) FROM test
```

이 경우에는 A값이 존재할 경우 A, 
A값이 null일 경우 B 값으로 대체해서 출력된다.

```sql
SELECT COALESCE(A, '---') FROM test;
```

이렇게 사용해서 A 값이 null일때,
'---'로 대체하여 출력할 수 있다.


<br>
<br>
<br>

## 조건에 맞는 도서 리스트 출력하기
- 문제
```
BOOK 테이블에서 2021년에 출판된 '인문' 카테고리에 속하는 도서 리스트를 찾아서 도서 ID(BOOK_ID), 출판일 (PUBLISHED_DATE)을 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.
```
- SQL
```sql
SELECT BOOK_ID, date_format(PUBLISHED_DATE,'%Y-%m-%d') as PUBLISHED_DATE
    FROM BOOK
    WHERE CATEGORY='인문' AND PUBLISHED_DATE LIKE '2021%';
```

<br>
<br>
<br>

## 조건에 부합하는 중고거래 댓글 조회하기
- 문제
```
USED_GOODS_BOARD와 USED_GOODS_REPLY 테이블에서 2022년 10월에 작성된 게시글 제목, 게시글 ID, 댓글 ID, 댓글 작성자 ID, 댓글 내용, 댓글 작성일을 조회하는 SQL문을 작성해주세요. 결과는 댓글 작성일을 기준으로 오름차순 정렬해주시고, 댓글 작성일이 같다면 게시글 제목을 기준으로 오름차순 정렬해주세요.
```
- sql
```
SELECT
    UB.TITLE,
    UR.BOARD_ID,
    UR.REPLY_ID,
    UR.WRITER_ID,
    UR.CONTENTS,
    DATE_FORMAT(UR.CREATED_DATE, '%Y-%m-%d') AS CREATED_DATE
FROM USED_GOODS_BOARD UB
JOIN USED_GOODS_REPLY UR
    ON UB.BOARD_ID = UR.BOARD_ID
WHERE YEAR(UB.CREATED_DATE) = 2022
  AND MONTH(UB.CREATED_DATE) = 10
ORDER BY UR.CREATED_DATE ASC, UB.TITLE ASC;
```

### YEAR(), MONTH(), DAY(), HOUR(), MINUTE(), SECOND()
SQL의 Date 타입에서 년도, 월, 일, 시, 분, 초 를 뽑을 때 사용.
결과 값은 Int 타입으로,
GROUB BY에 사용되기도 한다.

- 특정 사용자가 등록한 게시글의 수를 연도별로 분류하여 조회하는 SQL
```sql
SELECT YEAR(created_date) AS Year, COUNT(*) AS TotalPosts
FROM posts
GROUP BY YEAR(created_date)
ORDER BY Year;
```

<br>
<br>
<br>

## 어린 동물 찾기
- 문제
```
동물 보호소에 들어온 동물 중 젊은 동물의 아이디와 이름을 조회하는 SQL 문을 작성해주세요. 이때 결과는 아이디 순으로 조회해주세요.
(젋은 : INTAKE_CONDITION이 Aged가 아닌 경우를 뜻함)
```
- SQL
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE NOT INTAKE_CONDITION='Aged'
ORDER BY ANIMAL_ID;
```

> WHERE에 not을 붙이면 해당 조건이 아닌 경우임.



