---
title: '[Laravel] Codeception'
date: 2020-05-25 16:42:00 -0400
categories: devlog
tags: laravel devlog codeception
---

# What is Codception ?
PHP에는 PHPUnit이라는 테스트 프레임워크가 있다. 하지만 PHPUnit으로 REST API를 테스트 하려면 번거롭다.

1개 API를 테스트 할때마다 json_encode, json_decode, curl_exec가 등장하면서 테스트 코드가 복잡해진다.

Codeception은 바로 이러한 REST API를 테스트하는데 최적화된 PHPUnit 기반의 프레임워크이다.
테스트 코드의 양이 줄면서 가독성이 증가하고 테스트 자체에 집중할 수 있다.

## Get Start
```
composer require codeception/codeception
```

PHPStorm 연동
```
File -> Settings -> Language & Frameworks -> PHP -> Codeception
-> Path to Codeception executable: {프로젝트 루트}/vendor/codeception/codeception/codecept.bat
```
