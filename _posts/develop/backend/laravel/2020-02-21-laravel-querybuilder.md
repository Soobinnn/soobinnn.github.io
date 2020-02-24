---
title: '[Laravel] Query Builder'
date: 2020-02-21 09:55:00 -0400
categories: devlog
tags: laravel devlog querybuilder query
---

# Laravel에서 DB 접근 방법

# 기본

## select

```php
DB::select('select * from table where column1 = ?', [1]);
```

## insert

```php
DB::select('select * from table where column1 = :id', ['id' => 1]);
```

## update

```php
DB::update('update table set column1 = 100 where column2 = ?', ['John']);
```

## delete

```php
DB::delete('delete from table');
```

## transaction

```php
// # 기본
try {
 DB::transaction(function() use() {
  // query작성
})
}catch(Exception $e) {

}
```

트랜잭션의 클로져에서는 클로져밖의 변수를 사용할 수 없다. 사용하기 위해서는 use 를 사용해야함.

```php
// # Example
try {
 $name = "hello"
 DB::transaction(function() use($name) {
  DB::select("select * from users where name=?", [$name])
})
}catch(Exception $e) {

}
```

# 쿼리 빌더 란?

PDO 파라미터 바인딩을 사용하여 SQL Injection 공격을 방지하기 위해 사용하며, sql을 간단하게 작성할 수 있다.

```php

```

# 참고 문서
