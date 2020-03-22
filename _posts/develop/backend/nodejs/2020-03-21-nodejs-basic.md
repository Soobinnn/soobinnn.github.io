---
title: '[Node.js] Basic'
date: 2020-03-21 11:00:00 -0400
categories: devlog
tags: nodejs devlog
---

# 기본 개념

1. I/O
2. 비동기/동기
3. Non-blocking / bloking

## I/O

nodejs를 창시한 이유

일반적인 Web application Server는 네트워크 요청(blocking)이 이루어지는 환경에서 해당하는 네트워크 요청이 완료되기 전까지 다음 단계를 넘어가지 못하고 Thread문제와 같은 동시성 문제가 있음.

이와 같은 동시성 프로그래밍에 있어서 문제를 해결하기 위해 시작함.

일반적인 Web Application의 중요한 요소
-> 네트워크 I/O 요청


## 동기

어떠한 요청이 있다면 반드시 그요청을 처리하는 다른 대상과 동일하게 될 동안 기다리는 것.

성능적인 문제에 단점이 됨.

## 비동기
완료되는 시점을 기다리지 않는다.

이벤트 루프 (V8엔진)에서 이뤄짐

## blocking
해당 하는 코드, 작업이 완료될 때까지 다른 작업, 요청을 처리하지 못한다는 의미

## Non-blocking
어떠한 작업이 하는 동안 기다리지 않고 같이 수행하는 의미

/* 자바스크립트 특성 Non-blocking -> Web Brower에서 사용하는 언어이기 때문

자바스크립트는 이벤트 주도 언어이다.

/* 쓰레드풀 기반
사용자가 반응을 이어갈 때까지 쓰레드에서 대기함.


use strict

# Node, Web Browser 차이

## Node

nodejs에서는 window를 사용할 수 없다.

```javascript
const dns = require('dns')
```

## Web Browser

window 객체는 web browser상의 화면으로 global 객체로 존재.

import 는 es6 버전 이후 문법


# REPL

1. 특정한 객체의 정보가 필요할 때
String.
Number.

2. 한 줄 단위로 코드를 실행하고 싶을 때

# npm
```
npm install express --save-dev

npm uninstall
```

# npx
설치하지 않고 해당 모듈을 1회성으로 실행하는 것이 목적

# nodemon
파일의 변화가 있을 때 nodemon은 변화를 감지해서 재실행 시킴.

## Get Starting
```
npm i nodemon -g
```
