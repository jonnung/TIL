# PostgreSQL DISTINCT

기본적으로 모든 열의 값이 정확히 일치하는 행만 중복으로 간주한다.  


## 일반적인 DISTINCT
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

- 지정된 모든 열의 값 조합이 고유한 행만 반환
- 모든 열에 대해 중복 제거가 적용됨
- 중복 제거만 가능하며 어떤 행이 선택될지 제어할 수 없음


## **DISTINCT ON**
```sql
SELECT DISTINCT ON (column1) column1, column2, ...
FROM table_name
ORDER BY column1, column2 [DESC];
```

- 여러 행 중에서 특정 컬럼 값을 기준으로 첫 번째 행만 선택하고 싶을 때 사용
- `column1` 값이 같은 행들 중에서 `ORDER BY` 에 지정된 정렬 순서에 따라 첫 번째 행만 선택
- 지정된 컬럼의 값만 고유하면 되며, 다른 컬럼은 중복될 수 있음

