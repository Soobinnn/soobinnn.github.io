---
title: '[Laravel] TEST'
date: 2020-01-15 14:21:00 -0400
categories: devlog
tags: spring devlog test tdd
---

# TDD 시작하기

## PHPUnit

```
composer create-project --prefer-dist laravel/laravel tdd-crud
```

- Unit 프로그래머 관점에서 작성됨. 클래스의 특정 메소드가 일련의 특정 테스크를 수행하도록 보장됨

- Feature

  사용자 관점에서 작성됨. 사용자가 기대하는대로 시스템이 작동하는지 확인함.

1. Setting

root 디렉토리에서 `phpunit.xml` 파일수정

```
...
<env name="DB_CONNECTION" value="sqlite"/>
<env name="DB_DATABASE" value=":memory:"/>
<env name="API_DEBUG" value="false"/>
<ini name="memory_limit" value="512M" />


    <env name="APP_ENV" value="testing"/>
    <env name="DB_CONNECTION" value="sqlite"/>
    <env name="DB_DATABASE" value=":memory:"/>
    <env name="BCRYPT_ROUNDS" value="4"/>
    <env name="CACHE_DRIVER" value="array"/>
    <env name="MAIL_DRIVER" value="array"/>
    <env name="QUEUE_CONNECTION" value="sync"/>
    <env name="SESSION_DRIVER" value="array"/>
...
```

데이터베이스에는 sqlite 데이터베이스와 :memory:를 사용함.

2. TestCase

기본적으로 `Feature` 와 `Unit` 두개의 폴더로 구성됨.

```
php artisan make:test <테스트케이스 명>
```

tests/features 폴더 안에 <테스트케이스명>으로 파일이 생성됨.

\* 테스트 파일은 <테스트케이스명>Test.php로 끝나야함.

```php

```

\$ this-> assertJson ([ 'key'=> 'value']);

\$ this-> assertDatabaseHas ( 'table', [ 'field'=> 'value']);

\$ this-> assertRedirect ( 'url');

## CodeCeption

테스트케이스명뒤에 Cest를 붙인다.

#### Controller

```php
   public function getDashboard(AcceptanceTester $I)
    {
        $I->haveHttpHeader('Content-Type', 'application/json');
        $I->sendGET('/v1/dashboards/1');
        $I->seeResponseIsJson(200);
        $I->seeResponseContainsJson(['error' => 0, 'status_code' => ResponseCode::HTTP_OK]);
    }
```

#### Service

```php

```

```php

```

\* 참고

[https://laravel.com/docs/5.6/http-tests#available-assertions](https://laravel.com/docs/5.6/http-tests#available-assertions)

https://codefrontback.com/2019/04/04/basic-crud-with-tdd-in-laravel-5-8-tutorial/
