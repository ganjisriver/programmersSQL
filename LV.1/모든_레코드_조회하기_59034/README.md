# 모든 레코드 조회하기

### 문제 링크

링크: https://school.programmers.co.kr/learn/courses/30/lessons/59034

### 키워드

정렬

## 문제 답변

### MySQL 답변

```sql
SELECT * FROM ANIMAL_INS;
```

- 중복 답안1 - ORDER BY 생략 가능

- ```sql
  SELECT * FROM ANIMAL_INS ORDER BY ANIMAL_ID; (ORDER BY 절 생략 가능)
  ```

### Oracle 답변

```sql
SELECT * FROM ANIMAL_INS ORDER BY ANIMAL_ID;
```

## MySQL과 Oracle 차이

MySQL의 경우 ORDER BY를 생략해도 ANIMAL_ID 오름차순으로 정렬해서 반환을 한다.

ORACLE의 경우, order by를 생략하면 오답처리 된다.

- MySQL에서는 기본적으로 insert 기준이 아닌 primary key 기준으로 반환해준다고 나와있지만, 정렬에 대한 요구 사항이 있다면, 반드시 order by를 사용하라고 말한다.

- Oracle도 기본적으로는 오름차순 정렬이라고 나와있고, order by를 생략해도 코드 실행 결과에서는 animal_id 기준으로 오름차순 정렬로 출력되지만, 어째선지 해당 문제에서는 통과되지 않는다. 

### 참고 자료

[1995 Dev :: Order by 제외시 정렬 기준](https://1995-dev.tistory.com/43#google_vignette)
