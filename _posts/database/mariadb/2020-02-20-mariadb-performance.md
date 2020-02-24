---
title: '[MariaDB] Performance'
date: 2020-02-20 19:44:00 -0400
categories: database
tags: mariadb database performance
---

# 성능

## Row Lookup

Paging을 할 때 LIMIT, OFFSET을 이용하여 구현하는 경우가 많습니다. 하지만 이 때 WHERE 조건이 색인이 걸린 부분이라 당연하게 최적화가 되었다고 생각하지만 중요한 부분을 놓치고 있었습니다.

바로 Row lookup으로 인한 성능 저하입니다. Row lookup은 색인이 가르키는 Row를 접근하여 가져오는 행위입니다. 즉 LIMIT, OFFSET을 통해 페이지를 하는 동안 지나치는 Row들을 바라보며(lookup) 성능이 느려지게 됩니다. 자세한 내용은 먼저 성능 결과를 확인한 뒤 파악하겠습니다.

검색 성능을 확인하기 위해 v1, 2, 3 세 가지 쿼리를 300만 건 가량의 Row가 있는 Table에 수행해봅니다. 단순히 빨라지는 것이 아니라 다음 그래프가 같이 페이지에 따라 급격한 속도 차이가 발생합니다.

## Tip

- ORDER BY 에 많은 비용이 발생한다.

- Index만 조회할때 더 빠른 속도를 보장한다

- ORDER BY DESC 는 비용이 더 든다.

- 일정이상 데이터가 많아짐에 따라 정렬에 필요한 리소스는 가파르게 증가한다.

## SQL Query

해당 방법은 index를 타지 않으므로 성능이 저하됨

```
SELECT *
FROM TABLE
LIMIT {OFFSET}, {LIMIT}
```

```
SELECT *
FROM TABLE
LIMIT {OFFSET}, {LIMIT} FORCE INDEX (PRIMARY)
```

대안1

```
SELECT *
FROM TABLE
WHERE {OFFSET} < KEY
LIMIT {LIMIT}
```

대안2 커버링 인덱스 쿼리

```
SELECT *
FROM (
    SELECT id
    FROM Position
    LIMIT 2000000, 1000
) q
JOIN Position p
ON p.id = q.id
```
