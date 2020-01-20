---
title: '[Spring] HATEOAS'
date: 2020-01-20 23:28:00 -0400
categories: devlog
tags: spring devlog hateoas
---

# HATEOAS 란?
Hypermedia As The Engine Of Application State

REST 아키텍쳐의 한 구성요소
Server 관점 : 현재 리소스와 연관된 링크 정보를 클라이언트에게 제공
Client 관점 : 연관된 링크 정보를 바탕으로 리소스에 접근한다.

HATEOAS를 통해서 어플리케이션의 상태를 전이 할 수 있는 메커니즘을 제공

RESTful API를 사용하는 클라이언트가 전적으로 서버에 의해 동적으로 상호작용을 할 수 있다. 클라이언트가 서버에 요청 시 서버는 요청에 의존되는 URI를 Response에 포함시켜 반환한다.


스프링에서는 스프링 HATEOAS라는 프로젝트를 통해 스프링 사용자들에게 HATEOAS 기능을 손 쉽게 쓸 수 있도록 제공하고 있다.

# 에제
## 전형적인 REST API Response
```
{
    "name" : "sbim"
}
```
## HATEOAS 
```
{
    "name" : "sbim"
    "links": [
    {
      "rel": "self",
      "href": "http://localhost:8080/user"
    },
    {
      "rel": "delete",
      "href": "http://localhost:8080/user/delete"
    },
    {
      "rel": "update",
      "href": "http://localhost:8080/user/update"
    }
  ]
}
```
HATEOAS를 보면 name이 존재하기 때문에, 삭제, 수정을 실행할 수 있는
API 엔드포인트르 확인이 가능함.
 rel 이름만 알면 해당 기능의 실행 가능 여부를 판단할 수 있게 됨.

-> 사용자 정보를 입력(POST)하는 요청 후 사용자를 조회(GET), 수정(PUT), 삭제(DELETE)할 수 있는 URI를 동적으로 알려주게 됨.

URI정보를 보여줄 때 장점
1. 요청 URI정보가 변경되어도 클라이언트에서 동적으로 생성된 URI를 사용한다면, 클라이언트 입장에서는 URI 수정에 따른 코드 변경이 불필요 하다.

2. URI 정보를 통해 의존되는 요청을 예측가능하게 한다.

3. 기본 URI정보가 아니라 resource까지 포함된 URI를 보여주기 때문에 resource에 대한 확실을 갖게 된다.