---
title: '[Spring] Spring Annotation'
date: 2020-05-06 15:03:00 -0400
categories: devlog
tags: spring devlog annotation
---

# Spring Mvc

## @Controller

MVC의 View를 사용

controller를 사용하면 @RequestMapping등의 추가적인 어노테이션을 사용할 수 있게 된다.

## @ControllerAdvice
@ExceptionHandler가 하나의 클래스에 대한 것이라면, @ControllerAdvice는 모든 @Cotroller즉, 전역에서 발생할 수 있는 예외를 잡아 처리해주는 annotation


## @PathVariable

URL에서 Path 파라미터를 받아서 사용.

## @RequestParam

파라미터를 받아올 때 사용


## @ResponseBody

http request body를 자바 객체로 변환

## @ResponseStatus

## @ExceptionHandler
@Controller, @RestController가 적용된 Bean내에서 발생하는 예외를 잡아서 하나의 메소드에서 처리해주는 기능

```java
@ExceptionHandler(NullPoitnerException.class)
public Object nullcheck(Exception e) {
  ....
}
```
- @Controller, @RestController에서만 적용가능하다
- Return 타입은 자유롭게 해도된다.



## @RestController

@Controller + @ResponseBody

Controller중 view로 응답하지 않는 컨트롤러

### \* @Contoller , @RestController 차이점

HTTP Response Body가 생성되는 방식의 차이

기존 @Controller는 MVC의 View를 사용

@RestController는 객체를 반환할 때 객체 데이터는 JSON/XML 타입의 HTTP Response를 반환함.

@Controller의 메소드에 @ResponseBody를 선언해서 객체를 리턴하는 방법과 동일

#### 실행 흐름

`@Controller`

Client -> Request -> Dispatch Servlet -> Handler Mapping -> Controller -> View -> Dispatcher Servlet -> Response -> Client

`@ResponseBody`

Client -> Request -> Dispatch Servlet -> Handler Mapping -> Controller(ResponseBody) -> Response -> Client

`@RestController`

Client -> Http Request -> Dispatcher Servlet -> Handler Mapping -> RestController (@ResponseBody Auto Add) -> Http Response -> Client

#### ResponseEntity

규약에 맞는 HTTP Response를 제공하기 위해

HttpEntity를 상속받음으로써 HttpHeader, body를 가질 수 있다.
```java
ResponseEntity.status(HttpStatus.Ok).body(vo)
```

##### property

status field를 가지기 때문에 상태코드는 필수로 리턴해줘야함.

|이름|Type|설명|
|----|----|----|
| statusCode | org.springframework.http.HttpStatus | 상태 코드 |
| headers | org.springframework.http.HttpHeaders | Http 응답 |
| body | T(ResponseEntity 오브젝트 생성 시 형 변수 지정) | Body에 삽입할 정보를 유지하는 오브젝트 |

# Meta Annotation

## @Retention
해당 어노테이션이 언제까지 유지할지 알려주는 어노테이션
자기자신이 어느 시점까지 유효한지 명시해야함
```
@Rentention(RentionPolicy.RUNTIME)
```
- RetentionPolicy.SOURCE : 컴파일 전까지만 유효 (컴파일 이후에 사라짐)
- RententionPolicy.CLASS : 컴파일러가 클래스를 참조할 때까지 유효
- RetentionPolicy.RUNTIME : 컴파일 이후에도 JVM에 의해 계속 참조가 가능 (리플렉션 사용)

## @Target
어노테이션이 적용할 위치를 선택
어노테이션이 생성될 수 있는 위치 지정

ElementType.PACKAGE : 패키지 선언
ElementType.TYPE : 타입 선언
ElementType.ANNOTATION_TYPE : 어노테이션 타입 선언
ElementType.CONSTRUCTOR : 생성자 선언
ElementType.FIELD : 멤버 변수 선언
ElementType.LOCAL_VARIABLE : 지역 변수 선언
ElementType.METHOD : 메서드 선언
ElementType.PARAMETER : 메소드의 파라미터로 선언된 객체에서만 사용 가능
ElementType.TYPE_PARAMETER : 전달인자 타입 선언
ElementType.TYPE_USE : 타입 선언


# etc

## @Value
프로퍼티 키를 사용하여 특정 값을 호출할 수 있다.

```
@Value("${property.test.url}")
private String url;
```

# 참고자료

https://velog.io/@adam2/%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98-%EB%AA%A8%EC%9D%8C%EC%A7%91-%EC%9E%90%EB%B0%94-%EB%A9%94%ED%83%80-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98