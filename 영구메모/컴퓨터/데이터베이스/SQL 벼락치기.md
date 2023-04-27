|                 |                         |
|:----------------|:------------------------|
|   작성일           |   2023-04-19   |
|     분류          |                         |
| 태그              ||  


# Select
---
```sql
-- 테이블 불러오기
select * from table

-- column 불러오기
select acol from tb
```

# WHERE
---
```sql
SELECT a FROM ta WHERE NOT a is NULL

SELECT * FROM FIRST_HALF WHERE FLAVOR = "VANILLA"
AND INGREDIENT_TYPE = 'FRUIT_BASED'
```

# join
---
```sql
-- ICECREAM_INFO.FLAVOR = FIRST_HALF.FLAVOR 같은 행끼리 join
SELECT FIRST_HALF.FLAVOR FROM FIRST_HALF 
    LEFT JOIN ICECREAM_INFO
    ON ICECREAM_INFO.FLAVOR = FIRST_HALF.FLAVOR
```


# DATE
---
```sql
--  날짜를 문자열로 출력
SELECT DATE_FORMAT('2019-09-16 20:23:12', '%Y/%M/%D')  

-- 문자열을 날짜로 변환
SELECT STR_TO_DATE('20080101', '%Y-%M-%D')  

YEAR(날짜) -- 2020

MONTH(날짜) -- 9

DAY(날짜) -- 29
```

# 정렬
---
```sql
-- 오름차순 정렬
ORDER BY 컬럼명

-- 오름차순 정렬
ORDER BY 컬럼명 DESC
```

# if
---
```sql
SELECT IFNULL(Column명, "Null일 경우 대체 값") FROM 테이블명

-- name 이 null 이면 no name, 아니면 name 값 출력
SELECT IF(IS NULL(NAME), "No name", NAME) as NAME
FROM ANIMAL_INS
```


```sql
--평균 구하기
AVG(column명)

--소수 반올림
ROUND()

--   PARK으로 시작하는 데이터 검색
select * from tbl_board where title like 'PARK%';
```

# 관련 링크
---


# 출처
---