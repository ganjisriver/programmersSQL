# 특정 옵션이 포함된 자동차 리스트 구하기

### MySQL

```sql
SELECT * FROM CAR_RENTAL_COMPANY_CAR C WHERE C.OPTIONS LIKE '%네비게이션%' ORDER BY CAR_ID DESC;

-- LIKE 문 활용
```

### Oracle

- MySQL과 동일

<br>

### 보면 좋은 내용

- Like 문법 활용

```sql
SELECT * FROM 테이블 WHERE 칼럼 LIKE 'PATTERN'
```

Pattern에는 "%"와 "\_"가 들어간다. "%"는 모든 문자, "\_"는 한 단어를 의미한다.

```sql
SELECT * FROM TABLE WHERE NAME LIKE '%라면%'
```

위와 같은 SQL문에서 TABLE 내에 진라면, 짜장라면, 진라면 큰컵 등 라면이 포함되는 NAME의 컬럼을 가져올 수 있다.

```sql
SELECT * FROM TABLE WHERE NAME LIKE '%라면'
```


위와 같이 라면 뒤에 있는 "%"기호를 제거하고, 앞에만 붙는다면 "진라면", "짜장 라면"과 같이 라면으로 끝나는 컬럼을 가져올 것이다.

```sql
SELECT * FROM TABLE WHERE NAME LIKE '_라면%'
```

위와 같이 사용하게 되면 라면 앞에 언더바가 한개이기 때문에, "진라면", "진라면 큰컵" 등의 컬럼이 불러올 것이고, 짜장라면 등의 컬럼은 라면 앞에 글자수가 2글자이기 때문에 짜장라면과 같은 글자를 가져오려면 '\_라면%' 대신 '\___라면%'처럼 언더바를 두개 사용해야 가져올 수 있게 된다.

### 참고 자료

[SQL LIKE 연산자 - 문자열 부분일치 검색 [ % / _ ]](https://lcs1245.tistory.com/entry/SQL-LIKE-%EC%97%B0%EC%82%B0%EC%9E%90-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%B6%80%EB%B6%84%EC%9D%BC%EC%B9%98-%EA%B2%80%EC%83%89)


