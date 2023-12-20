# 조건에 부합하는 중고거래 댓글 조회하기

## 문제 답변

### MySQL 답변

```sql
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS CREATED_DATE
FROM USED_GOODS_BOARD B JOIN USED_GOODS_REPLY R ON b.BOARD_ID = r.BOARD_ID
WHERE B.CREATED_DATE LIKE "2022-10%" ORDER BY R.CREATED_DATE, B.TITLE
```

### Oracle 답변

```sql
SELECT B.TITLE 
```

- WHERE 절에 BETWEEN도 가능

<br>

## MySQL과 Oracle 차이

- 날짜 Formatting

<br>

### 보면 좋은 내용
