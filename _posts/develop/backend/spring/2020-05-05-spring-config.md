---
title: '[Spring] Config Setting'
date: 2020-05-05 21:52:00 -0400
categories: devlog
tags: spring devlog config setting
---

# Spring 설정

## .xml

## .yml

## Java Config

Srping JavaConfig는 XML이 아닌 자바 코드를 이용해서 컨테이너를 설정할 수 있는 기능을 제공

- @Configuration
어노테이션기반 환경구성을 도움.

이 어노테이션을 구현함으로써 클래스가 하나 이상의 @Bean메소드를 제공하고 요청을 처리할 것을 선언하게됨.

import org.springframework.context.annotation 패키지에 존재


- @Bean

새로운 빈 객체를 제공할 때 사용,
@Bean이 적용된 메서드의 이름을 빈의 식별값으로 사용함.

```java
// XML
<bean id="alarmDevice" class="mad.spring.ch4.homecontrol.SmsAlarmDevice"/>


// Java
//alarmDevice이 아닌 smsAlarmDevice을 사용하고 싶은 경우
@Bean(name="smsAlarmDevice")
public AlarmDevice alarmDevice(){
	return new SmsAlarmDevice();
}
```

# 참고 문서
https://devbox.tistory.com/entry/Spring-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C-%EA%B8%B0%EB%B0%98-%EC%84%A4%EC%A0%95