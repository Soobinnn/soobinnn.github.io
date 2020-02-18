---
title: '[MariaDB] Query / Command'
date: 2020-02-02 13:00:00 -0400
categories: database
tags: mariadb database command
---

# Query

## Join

JOIN은 집합간의 곱이다 1:1 관계 테이블이 조인하면 1*1 레벨의 집합이 생성되고, 1:M관계가 조인하면 1*M 레벨의 집합이된다. M\*N 관계 테이블이 조인하면 MN 레벨의 집합이 된다.

## SubQuery

서브쿼리는 메인쿼리의 컬럼을 모두 사용할 수 있지만, 메인 쿼리는 서브 쿼리의 컬럼을 사용할 수 없다.

서브쿼리는 서브쿼리 레벨과는 상관없이 항상 메인쿼리 레벨로 결과 집합이 생성된다.

### 주의사항

- 서브쿼리를 괄호로 감싸서 사용한다
- 서브쿼리는 단일 행 또는 복수 행 비교 연산자와 함꼐 사용 가능
- 서브쿼리에는 ORDER BY를 사용하지 못한다.

### 종류

1. 단일행 서브쿼리

```
SELECT *
FROM BOARD
WHERE CATEGORY_ID = (
  SELECT ID
  FROM CATEGORY
  WHERE CATEGORY_NAME = "FREE"
)
```

2. 다중행 서브쿼리

```
SELECT *
FROM BOARD
WHERE CATEGORY_ID IN (
  SELECT ID
  FROM CATEGORY
  WHERE CATEGORY_NAME = "FREE"
)
```

3. 다중컬럼 서브쿼리

```

```

# 명령어

```
# DB 생성
CREATE DATABASE <db명>;

# DB 보기
show databases;

# 특정 DB 사용하기
use <dbname>
```
