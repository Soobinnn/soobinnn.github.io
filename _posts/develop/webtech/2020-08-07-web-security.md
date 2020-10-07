---
title: '[Web] Security'
date: 2020-03-31 15:38:00 -0400
categories: devlog
tags: web devlog Security
---

# Web Security

## XSS

공격자가 클라이언트 브라우저에 javascript를 삽입해 실행하는 공격.

공격자가 `<input/>`을 통해 Javascript를 서버로 전송해 서버에서 스크립트를 실행하거나 url에 javascript를 적어 클라이언트에서 스크립트를 실행이 가능하다면 공격자가 사이트 스크립트를 삽입해 XSS 공격을 할 수 있다.

이 때 공격자는 Javascript를 통해 사이트 글로벌 변수값을 가져오거나 그 값을 이용해 사이트인 척 API콜을 요청할 수도 있다. -> 공격자의 코드가 내 사이트의 로직인 척 행동할 수 있다.

## CSRF

공격자가 다른 사이트에서 우리 사이트의 API를 요청해 실행하는 공격.

API를 요청할 수 있는 클라이언트 도메인이 누구인지 서버에서 통제하고 있지 않다면 CSRF가 가능한데, 이때 공격자가 클라이언트에 저장된 유저 인증정보를 서버에 보낼 수 있다면, 제대로 로그인한 것처럼 유저의 정보를 변경하거나 유저만 가능한 액션들을 수행할 수 있다.