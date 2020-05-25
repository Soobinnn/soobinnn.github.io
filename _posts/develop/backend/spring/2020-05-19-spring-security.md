---
title: '[Spring] Spring Security'
date: 2020-05-19 20:47:00 -0400
categories: devlog
tags: spring devlog security 
---
# Security
- 인증
- 인가

## Authenticatioon (인증)
  증명하다. 라는 의미로, 로그인하는 과정

## Authorization (인가)
  권한부여, 허가와 같은 의미로, 어떤 대상이 특정 목적을 실현하도록 허용하는 것을 의미.

* Web에서 `인증`은 해당 URL은 보안 절차를 거친 사용자들만 접근할 수 있다는 의미,

`인가`란 URL에 접근한 사용자가 특정한 자격이 있다는 것을 의미


# Spring Security

WebSecurityConfigurerAdapter는 세가지 configure메소드를 오버라이딩하고 동작을 설정하는 것으로 웹 보안을 설정할 수 있다.


configure(WebSecurity)
 
 스프링 시큐리티의 필터 연결을 설정하기 위한 오버라이딩

configure(HttpSecurity)

인터셉터로 요청을 안전하게 보호하는 방법을 설정하기 위한 오버라이딩

configure(AuthenticationManagerBuilder)

사용자 세부 서비스를 설정하기 위한 오버라이딩





## Annotation
- @EnableWebSecurity
- EnableWebMvcSecurity

### @EnableWebSecurity

웹 보안을 활성화.

그자체로는 유용하지 않고, 스프링 시큐리티가 WebSecurityConfigurer를 구현하거나 컨텍스트의 WebSecurityConfigurerAdapter를 확장한 빈으로 설정되어 있어야 한다.

 WebSebSecurityConfigurerAdapter를 확장하여 클래스를 설정하는 것이 가장 편하고 자주 쓰이는 방법이다.

### @EnableWebMvcSecurity

스프링 MVC 인수 결정자를 설정하여, 핸들러 메소드가 @AuthenticationPrincipal이 붙은 인자를 사용하여 인증한 사용자 주체를 받는다.

또한 자동으로 숨겨진 사이트 간 요청 위조(CSRF, Cross-Site Request Forgery) 토큰필드(token field)를 스프링의 폼 바인딩 태그 라이브러리를 사용하여 추가하는 빈을 설정한다.

## Setting

- Gradle
```
compile group: "org.springframework.boot", name: "spring-boot-starter-security"
```

- Java Config
```java
@Configuration
@EnableWebSecurity
public class SecurityJavaConfig extends WebSecurityConfigurerAdapter {

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http
        .cors().disable()
        .csrf().disable()
        .formLogin().disable();
  }
}
```

## 