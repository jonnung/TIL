# TIL-20190801/Postgresql: Queries VALUES

## `VALUES` Lists

DB에 저장되는 실제 테이블을 만들지(`CREATE`) 않고, 고정된 데이터로 테이블을 만들어서 사용할 수 있는 방법

▶︎ 문법

    VALUES ( expression [, ...] ) [, ...]

괄호로 감싸진 데이터 쌍(ex: `('A', 'B')`)을 담은 리스트가 테이블의 각 row가 된다.

리스트 안에 데이터 쌍이 갖는 값의 개수는 전부 같아야 한다. 그리고 같은 순서에 있는 값들은 서로 동일한 data type이여야 한다.

▶︎ 예시

    VALUES (1, 'one'), (2, 'two'), (3, 'three'); 

위 쿼리 결과는 아래 쿼리와 동일하고, 자동으로 `column1`, `column2` 라는 컬럼명이 부여된다. 

    SELECT 1 AS column1, 'one' AS column2
    UNION ALL
    SELECT 2, 'two'
    UNION ALL
    SELECT 3, 'three';

하지만 표준 SQL이나 다른 DB에서는 컬럼명을 지정 해주지 않기 때문에 테이블 Alias를 통해 컬럼명을 오버라이드 해주는 것이 좋다.

    SELECT * FROM (VALUES (1, 'one'), (2, 'two'), (3, 'three')) AS t (num,letter);

`VALUES`의 결과는 아래와 같이 `SELECT` 문과 동등하게 어디든 사용될 수 있다.

- `UNION`의 일부분으로 사용 가능
- `ORDER BY`, `LIMIT`또는 `OFFSET` 에 지정
- `INSERT` 에 데이터 소스로 사용
- Subquery에 활용

참고: [https://www.postgresql.org/docs/9.6/queries-values.html](https://www.postgresql.org/docs/9.6/queries-values.html)