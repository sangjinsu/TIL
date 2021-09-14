# DB

데이터베이스

- 체계화된 데이터 모임
- 자료 항목의 **중복을 없애고** 자료를 **구조화**하여 기억하는 자료의 집합체

### 장점

- 데이터 중복 최소화
- 데이터 무결성
- 데이터 일관성
- 데이터 독립성 (물리적, 논리적)
- 데이터 표준화
- 데이터 보안 유지

## 관계형 데이터베이스

- 키와 값들의 간단한 관계를 표 현태로 정리한 데이터베이스
- 관계형 모델 기반 

### 스키마

- 데이터베이스에서 자료 구조, 표현 방법, 관계 등 전반적인 명세를 기술한 것

### 테이블

- 테이블: 열과 행 모델을 사용해 조직된 데이터 요소들의 집합 
- 열: 각 열에는 고유한 데이터 형식이 지정됨
- 행: 실제 데이터 저장 형태
- 기본키: 각 행 고유값, 반드시 설정해야 하며 데이터 관리 및 관계 설정시 주요하게 활용된다

## RDBMS

- 관계형 모델을 기반으로하는 데이터베이스 관리 시스템

## SQL

- 데이터 관리를 위한 특수 목적 프로그래밍 언어

  ### DDL 데이터 정의 언어

  - 관계형 데이터베이스 구조를 정의하기 위한 명령어
  - CREATE, DROP, ALTER

  ### DML 데이터 조작 언어

  - 데이터 저장, 조회, 수정, 삭제 등을 하기 위한 명령어
  - INSERT, SELECT, UPDATE, DELETE

  ### DCL 데이터 제어 언어

  - 데이터베이스 사용자 권한 제어에 의해 사용되는 명령어
  - GRANT, REVOKE, COMMIT, ROLLBACK

## SQLITE

- `.headers on` - 헤더 보이기

- `.mode column` - 열로 보이기 
- `.mode csv` - 불러올 파일 형식 

- `.import [csv 파일] [table 이름]` - csv 파일에서 테이블 가져오기 
- `.tables` - table 보기 

### TABLE

- CREATE TABLE 
- DROP TABLE

- `.schema [table 이름]` - schema 조회

- `INSERT INTO [table 이름] (컬럼) values (값)`

- ```sql
  SELECT rowid, -- sqlite 는 따로 primary 키를 정하지 않으면 값이 자동으로 증가하는 rowid 속성을 추가한다
  
   *
  
  FROM classmates;
  ```

## READ

- LIMIT 숫자 OFFSET 숫자 - 행 수 제한

  세번째에 있는 한 행 `LIMIT 1 OFFSET 2`

- WHERE - 조건문 

- DISTINCT - 조회 결과에서 중복 제거 

## DELETE

- DELETE FROM [테이블 이름] WHERE [조건];

### AUTOINCREMENT

- SQLITE 가 사용하지 않은 값이나 이전에 삭제된 행의 값을 재사용하는 것을 방지한다 
- column 속성으로 들어간다 

## UPDATE

- UPDATE [테이블 이름] SET 칼럼 = 값... WHERE 조건

## Aggregation

- COUNT, AVG, MAX, MIN, SUM

```sqlite
SELECT first_name,
  balance
FROM users
WHERE balance = (
    SELECT MAX(balance)
    FROM users
  );
```

## SQLITE 특징점

```sqlite
CREATE TABLE tableN (id INTEGER, name TEXT);

INSERT INTO tableN
VALUES (1, 'TEXT'),
  ('2', 10.1),
  ('2', 10.),
  ('2', 10),
  ('2b', 'TEST');
  
SELECT id,
  typeof(id),
  name,
  typeof(name)
FROM tableN;
```

```bash
id          typeof(id)  name        typeof(name)
----------  ----------  ----------  ------------
1           integer     TEXT        text
2           integer     10.1        text
2           integer     10.0        text
2           integer     10          text
2b          text        TEST        text  
```

- sqlite 는 다른 RDBMS 와 다르게 형식을 변환하여 저장한다.

- 불안전한 데이터가 삽입 될 수 있다

- > 매우 놀랐다...



## LIKE

- 패턴 일치를 기반으로 데이터를 조회하는 방법
- sqlite 는 패턴 구성을 위한 2 개의 wildcards 를 제공
  - % - 0개 이상의 문자
  - _ - 임의의 단일 문자

## ORDER BY

- 조회 결과 집합을 정렬

- ASC 오름차순

- DESC  내림차순 

  

## GROUP BY

- 행 집합에서 요약 행 집합을 만듦
- SELECT 문의 optional 절
- 문장에 WHERE 절이 포함된 경우 반드시 WHERE 절 뒤에 작성해야 한다

## ALTER TABLE

1. 테이블 이름 변경

2. 테이블에 새로운 COLUMN 추가 (DEFAULT 값 설정 가능)

   ```sqlite
   ALTER TABLE [테이블 이름]
   RENAME COLUMN [현재 이름] TO [바꿀 이름];
   
   ALTER TABLE [테이블 이름]  RENAME TO [새로운 테이블 이름];
   
   ALTER TABLE news ADD COLUMN created_at TEXT;
   
   ALTER TABLE news
   ADD COLUMN subtitle TEXT NOT NULL DEFAULT '소제목';
   ```

   

