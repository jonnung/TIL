# SQL 모드

MySQL 서버는 서로 다른 SQL 모드 상태에서 동작할 수 있다.
서로 다른 클라이언트에 대해 SQL 모드들을 서로 다르게 적용할 수 있다는 것이다.

## 모드(mode)란?
MySQL이 어떤 SQL Syntax를 지원하고 있는지 그리고 데이터의 유효성을 검사하는 방법은 무엇인지를 가리키는 것.

## 설정
- mysqld 를 `--sql-mode="modes"`옵션과 함께 구동
- my.cnf (윈도우는 my.ini)에 `sql-mode="modes"` 형태로 추가 후 `serviece mysql restart`
- `SET [GLOBAL|SESSION]` 명령문으로도 변경 가능.
GLOBAL 변수 설정은 SUPER 권한이 필요하다.
```
SET @@global.sql_mode='';
SET @@session.sql_mode='';

-- 현재의 GLOBAL, SESSION을 확인려면
SELECT @@global.sql_mode;
SELECT @@session.sql_mode;
```
참고: _`modes` 는 콤마(,)로 구분되는 서로 다른 모드들의 리스트_

## sql_mode 값
모드값에 대한 전체적인 내용을 확인하려면 [링크](http://www.mysqlkorea.com/sub.html?mcode=manual&scode=01_1&m_no=22283&cat1=752&cat2=790&cat3=868&lang=k)를 확인.
여기서는 스트릭트 모드(strict mode)에 대해 다룬다.
스트릭트 모드(strict mode)는 `STRICT_TRANS_TABLES` 또는 `STRICT_ALL_TABLES` 중에 하나가 활성화 되어 있는 곳의 모드를 말하며, MySQL이 유효하지 않거나 누락된(missing) 데이터를 처리하는 방법을 제어한다.

- **STRICT_ALL_TABLES**: 에러를 리턴하고 나머지 열들은 무시. 앞서 INSET/UPDATE한 열들은 그대로 적용된다.  
이런 상황을 피하기 우해서는 단일 명령문을 사용하는 것이 최선.
- **STRICT_TRANS_TABLES**: 유효하지 않은 값을 컬럼에 대해 가장 근접한 유효값으로 변환 시킨 다음에 값을 삽입한다. 데이터 값이 누락될 경우에는 MySQL은 컬럼 데이터 타입에 대한 암시적인(implicit) 디폴트 값을 삽입한다.  
두 경우 모드 MySQL은 에러가 아닌 경고 메세지를 출력한다.

스트릭트 모드를 사용하지 않는다면 MySQL은 유효하지 않거나 누락된 데이터 값을 적당히 유효하게 변환 시킨 값으로 삽입하고 경고문을 발생한다.



