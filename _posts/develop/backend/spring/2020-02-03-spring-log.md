---
title: '[Spring] Logging '
date: 2020-02-03 12:10:00 -0400
categories: devlog
tags: spring devlog log boot logback
---

# Spring boot logback 설정
spring-boot-starter-web 안에 spring-boot-starter-logging 구현체가 있다.

classpath에 logback-spring.xml이 있으면, boot는 설정파일을 읽음.

logback-spring.xml이 없다면 yml파일 설정을 봄.

logback-spring.xml파일과 .yml파일이 동시에 있다면 .yml 설정 파일을 먼저 적용 후 xml파일이 적용되는 것을 확인함.

## xml설정
```
<appender name="privateLogAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
  <file>${LOG_PATH}/private.${port:-default}.log</file>
  <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
    <fileNamePattern>${LOG_PATH}/private.${port:-default}.log.%d{yyyy-MM-dd}</fileNamePattern>
    <maxHistory>7</maxHistory>
  </rollingPolicy>
  <encoder>
    <pattern>%replace(%msg){'\n', ' '}%n</pattern>
  </encoder>
</appender>
```

## yml 설정
```
spring:
  profiles: default
  jackson.serialization.FAIL_ON_EMPTY_BEANS: false
logging:
  path: logs //이 값이 ${LOG_PATH}로 들어가게됨.
  level.org.hibernate:
    SQL: DEBUG
    type.descriptor.sql.BasicBinder: TRACE
```


# log 정보
- TRACE : 추적 레벨은 Debug보다 좀더 상세한 정보를 나타냅니다.
- DEBUG : 프로그램을 디버깅하기 위한 정보를 표시합니다. (운영서버에서는 표시하지 않도록 설정함)
- INFO  : 상태변경과 같은 정보성 로그를 표시합니다.
- WARN  : 처리 가능한 문제, 향후 시스템 에러의 원인이 될 수 있는 경고성 메시지를 나타냄 
- ERROR : 요청을 처리하는 중 오류가 발생한 경우 표시합니다.

# 설정
ch.qos.logback.core.ConsoleAppender : 콘솔에 로그를 찍음

ch.qos.logback.core.FileAppender : 파일에 로그를 찍음

ch.qos.logback.core.rolling.RollingFileAppender : 여러개의 파일을 순회하면서 로그를 찍음

ch.qos.logback.classic.net.SMTPAppender : 로그를 메일에 찍어 보냄

# 참고 자료
https://romeoh.tistory.com/entry/Spring-Boot-Logback-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0

https://jeong-pro.tistory.com/154