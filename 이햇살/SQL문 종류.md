# SQL문 종류

### 1. DDL(Data Define Language, 데이터 정의어)

- SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 `정의`하거나 `변경` 또는 `삭제`할 때 사용하는 언어

- 논리적 데이터 구조와 물리적 데이터 구조의 사상을 정의

- 데이터베이스 관리자나 데이터베이스 설계자가 사용

  | **명령어** | **기능**                                           |
  | ---------- | -------------------------------------------------- |
  | **CREATE** | SCHEMA, DOMAIN, TABLE, VIEW, INDEX 정의 ex) CREATE |
  | **ALTER**  | TABLE에 대한 정의를 변경                           |
  | **DROP**   | SCHEMA, DOMAIN, TABLE, VIEW, INDEX 삭제            |

### 2. DML(Data Manipulation Language, 데이터 조작어)

- 데이터베이스 사용자가 응용 프로그램이나 질의어를 통하여 `저장된 데이터를 실질적으로 처리`하는 데 사용하는 언어

- 데이터베이스 사용자와 데이터베이스 관리 시스템 간의 `인터페이스를 제공`

  | **명령어** | **기능**                                  |
  | ---------- | ----------------------------------------- |
  | **SELECT** | 테이블에서 조건에 맞는 튜플 검색          |
  | **INSERT** | 테이블에 새로운 튜플 삽입                 |
  | **DELETE** | 테이블에서 조건에 맞는 튜플 삭제          |
  | **UPDATE** | 테이블에서 조건에 맞는 튜플의 내용을 변경 |

#### 2.1 `SELECT`

가장 기본인 데이터를 불러오는 쿼리문

```sql
SELECT 컬럼명 FROM 테이블명
```

- 테이블명에 해당하는 테이블의 칼럼명에 데이터를 불러오는 구문
- 모든 칼럼을 불러오고 싶을 때는 컬럼 명 부분에 `*` 

```sql
SELECT 컬럼명 FROM 테이블명 WHERE 조건
```

- WHERE 구문을 추가해서 `WHERE절 뒤에 오는 조건이 참`인 데이터만 불러옴
- `컬럼명 = 값`으로 적을 경우 컬럼 명의 값이 지정한 값인 데이터행의 데이터만 불러옴

```sql
SELECT 컬럼명 FROM 테이블명 WHERE 조건 ORDER BY 컬럼명 ASC or DESC
```

- ORDER BY 뒤에 오는 칼럼명을 기준으로 데이터 정렬
  - `ASC`는 오름차순, `DESC` 내림차순
  - 기본값은 오름차순

```sql
SELECT 컬럼명 FROM 테이블명 WHERE 조건 ORDER BY 컬럼명 ASC or DESC LIMIT 개수
```

- LIMIT 구문을 추가하여 LIMIT 절의 개수만큼 데이터를 불러옴

#### 2.2 `INSERT`

데이터를 삽입하는 쿼리문

```sql
INSERT INTO 테이블명 (컬럼명1, 컬럼명2, 컬럼명3) VALUES (값1, 값2, 값3)
```

- 테이블명에 있는 칼럼명에 순서에 맞게 값을 입력

- 칼럼명과 값의 개수는 동일해야함

- 문자열을 값으로 입력하는 경우에는 작은따옴표로 문자열 감싸줘야 함

  ``` sql
  ex) INSERT INTO Employees (Employee_id, First_name, Last_name) VALUES (100, 'Aiden', 'Lee');
  ```

```sql
INSERT INTO 테이블명 VALUES (값1, 값2, 값3)
```

- 테이블명 다음에 칼럼명을 입력하지 않은 경우 테이블에 모든 칼럼에 값을 입력한다는 의미로 `모든 칼럼의 수에 맞게 값`을 줘야 함

  ```sql
  ex) 칼럼이 Employee_id, First_name, Last_name 3개인 테이블에서
  INSERT INTO Employees VALUES (100, 'Aiden') -> '잘못된 형식'
  INSERT INTO Employees VALUES (100, 'Aiden', 'Lee') -> '정답!'
  ```

#### 2.3 `UPDATE`

데이터를 수정하는 쿼리문

```sql
UPDATE 테이블명 SET 칼럼명 = 변경할 값
```

- 테이블에 있는 모든 데이터의 칼럼 값을 변경

```sql
UPDATE 테이블명 SET 칼럼명 = 변경할 값 WHERE 조건
```

- WHERE 절에 조건에 해당하는 데이터만 변경
  - ex) WHERE 컬럼명 = 값

```sql
UPDATE 테이블명 SET 칼럼명1 = 변경할 값1, 칼럼명2 = 변경할 값2 WHERE 조건
```

- 변경할 칼럼이 여러개일때 콤마( , )를 사용하여 여러 개 값 변경 가능

#### 2.4 `DELETE`

테이블에 데이터를 삭제하는 쿼리문

```sql
DELETE FROM 테이블명
```

- 테이블에 있는 모든 데이터 삭제

```sql
DELETE FROM 테이블명 WHERE 조건
```

- WHERE절의 조건에 맞는 데이터만 삭제

### 3. DCL(Data Manipulation Language, 데이터 제어어)

- 데이터의 보안, 무결성, 회복, 병행 수행 제어 등을 `정의`하는 데 사용되는 언어

- 데이터 베이스 관리자가 데이터 관리를 목적으로 사용

  | **명령어**   | **기능**                                                     |
  | ------------ | ------------------------------------------------------------ |
  | **COMMIT**   | 명령에 의해 수행된 결과를 실제 물리적 디스크로 저장하고, 데이터베이스 조작 작업이 정상적으로 완료되었음을 관리자에게 알려줌 |
  | **ROLLBACK** | 데이터베이스 조작 작업이 비정상적으로 종료되었을 때 원래 상태로 복구 |
  | **GRANT**    | 데이터베이스 사용자의 사용 권한 부여                         |
  | **REVOKE**   | 데이터베이스 사용자의 사용 권한 취소.                        |

---

참고자료

[SQL문 총 정리!!(Feat. SQL문 정리 사이트)](https://comclothing.tistory.com/74)

[기본 SQL Query문 정리 (SELECT, INSERT, UPDATE, DELETE)](https://lcs1245.tistory.com/entry/%EA%B8%B0%EB%B3%B8-SQL-Query%EB%AC%B8-%EC%A0%95%EB%A6%AC-SELECT-INSERT-UPDATE-DELETE#recentComments)

