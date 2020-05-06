---
title: '[Spring] Config Setting'
date: 2020-05-05 21:52:00 -0400
categories: devlog
tags: spring devlog config setting
---

# Spring 설정

## Java Config

### Spring Security

스프링 기반의 애플리케이션의 보안(인증, 권한,인가)를 담당하는 스프링 하위 프레임워크


__@EnableWebSecurity__

WebSecurityConfigurerAdapter를 상속받은 후 어노테이션 명시 -> springSecurityFilterChain 포함됨.

__WebSecurityConfigurerAdapter__

WebSecurityConfigurer 인스턴스 를 만들기위한 편리한 기본 클래스를 제공

구현은 메소드를 대체하여 사용자 정의를 허용

# 참고 문서
https://m.blog.naver.com/kimnx9006/220633299198

https://velog.io/@jayjay28/2019-09-04-1109-%EC%9E%91%EC%84%B1%EB%90%A8