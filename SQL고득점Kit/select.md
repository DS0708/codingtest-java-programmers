# SQL 고득점 kit - SELECT

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


