---
title: '[Spring] Spring Annotation'
date: 2020-05-06 15:03:00 -0400
categories: devlog
tags: spring devlog annotation
---

## @Controller

MVC의 View를 사용

## @ControllerAdvice

## @ResponseBody

## @ResponseStatus

## @ExceptionHandler

## @RestController

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

