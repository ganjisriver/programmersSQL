# 조건에 부합하는 중고거래 댓글 조회하기

### 문제 링크

링크: https://school.programmers.co.kr/learn/courses/30/lessons/164673

<BR>

### 키워드

**날짜 형식 출력 및 비교**

<BR>

## 문제 답변

### MySQL 답변

```sql
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS CREATED_DATE
FROM USED_GOODS_BOARD B JOIN USED_GOODS_REPLY R ON b.BOARD_ID = r.BOARD_ID
WHERE B.CREATED_DATE LIKE "2022-10%" ORDER BY R.CREATED_DATE, B.TITLE;
```

<br>

- 중복 답안1 -  LIKE를 사용하고, DATE_FORMAT 사용하여 비교

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE DATE_FORMAT(B.CREATED_DATE, "%Y-%m") LIKE '2022-10%'
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```

<br>

- 중복 답안2 - BETWEEN을 사용한 날짜 비교

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE B.CREATED_DATE BETWEEN '2022-10-01' AND '2022-10-31'
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```

<br>

- 중복 답안3 - YEAR, MONTH 함수 사용

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE MONTH(B.CREATED_DATE) = 10 AND YEAR(B.CREATED_DATE) = 2022
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```

<BR>

### Oracle 답변

```sql
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, TO_CHAR(R.CREATED_DATE, 'YYYY-MM-DD') AS CREATED_DATE
FROM USED_GOODS_BOARD B
JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
WHERE TO_CHAR(B.CREATED_DATE, 'YYYY-MM') = '2022-10'
ORDER BY R.CREATED_DATE, B.TITLE;
```

<br>

- 중복 답안 1 - LIKE를 사용한 비교 연산

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, TO_CHAR(R.CREATED_DATE, 'YYYY-MM-DD') AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE TO_CHAR(B.CREATED_DATE, 'YYYY-MM') LIKE '2022-10%'
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```

<BR>

- 중복 답안 2 - BETWEEN 사용 비교 연산

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, TO_CHAR(R.CREATED_DATE, 'YYYY-MM-DD') AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE B.CREATED_DATE BETWEEN TO_DATE('2022-10-01', 'YYYY-MM-DD') AND TO_DATE('2022-10-31', 'YYYY-MM-DD')
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```
  
  <BR>

- 중복 답안 3 - YEAR, MONTH, EXTRACT 함수 사용

- ```sql
  SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, TO_CHAR(R.CREATED_DATE, 'YYYY-MM-DD') AS CREATED_DATE
  FROM USED_GOODS_BOARD B
  JOIN USED_GOODS_REPLY R ON B.BOARD_ID = R.BOARD_ID
  WHERE EXTRACT(MONTH FROM B.CREATED_DATE) = 10 AND EXTRACT(YEAR FROM B.CREATED_DATE) = 2022
  ORDER BY R.CREATED_DATE, B.TITLE;
  ```

<br>

## MySQL과 Oracle 차이

**날짜 Formatting**

<br>

해당 답안 차이에서 눈 여겨 볼 것은 날짜 포맷에 있다. 

MySQL, Oracle 답안 모두 컬럼으로 가져올 때, 날짜 형변환을 거친다. 이 부분은 문제에서 날짜 관련 컬럼을 'YYYY-MM' 의 형태로 가공해서 가져오길 바랐기 때문에 해당 형태로 가져왔고, 그대로 가져와도 문제를 일으키지는 않는다.

큰 문제는 `WHERE 절에서의 비교`에 있다.

<br>

- **WHERE 절에서의 비교 연산**

<BR>

MySQL에서는 해당 컬럼을 문자열로 변경하지 않고, LIKE를 문자열로 사용해도 적용이 된다.

```sql
WHERE B.CREATED_DATE LIKE "2022-10%" -- MYSQL
```

Oracle의 경우에서 위와 같이 사용하면 오류를 발생시킨다. 날짜 형식에서 LIKE는 사용할 수 없기 때문이고, 아래처럼 날짜 컬럼을 문자열 형태로 바꿔주어야 LIKE 연산이 가능하다.

```sql
WHERE TO_CHAR(B.CREATED_DATE, 'YYYY-MM') LIKE '2022-10%' -- ORACLE
```

역으로, ORCALE에서 다음과 같이 문자를 날짜형식처럼 바꿔주면 컬럼을 문자열로 바꾸지 않아도 된다.

```sql
WHERE B.CREATED_DATE BETWEEN TO_DATE('2022-10-01', 'YYYY-MM-DD') AND TO_DATE('2022-10-31', 'YYYY-MM-DD')
```

<br>

- **MONTH, YEAR연산 차이**

MySQL은 Oracle과 달리 MONTH와 YEAR 함수를 사용할 때 그냥 다음과 같이 사용할 수 있다.

```sql
WHERE MONTH(B.CREATED_DATE) = 10 AND YEAR(B.CREATED_DATE) = 2022
```

하지만, Oracle의 경우 EXTRACT함수를 사용함으로써 특정 연,월,시간 등을 추출한다.

```sql
WHERE EXTRACT(MONTH FROM B.CREATED_DATE) = 10 AND EXTRACT(YEAR FROM B.CREATED_DATE) = 2
```

위처럼 EXTRACT(field FROM source)의 형태로 사용할 수 있다.



<br>

### 참고 자료

<br>

**MySQL 날짜 포맷 정리**

https://velog.io/@donghoim/MySQL-DATETIME-원하는-유형으로-변경-YYMMDD

**MySQL 날짜 관련 함수 공식 문서**

[MySQL :: MySQL 8.0 Reference Manual :: 12.7 Date and Time Functions](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)

<br>

**Oracle 날짜 포맷 정리**

[[Oracle] 날짜형, 숫자형의 포맷(Format)형식](https://kr98gyeongim.tistory.com/100)

**Oracle 날짜 포맷 공식 문서**

[Format Models](https://docs.oracle.com/database/121/SQLRF/sql_elements004.htm#SQLRF00211)
