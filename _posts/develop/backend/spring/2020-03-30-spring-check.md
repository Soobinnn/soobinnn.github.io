---
title: '[Spring] Code Check'
date: 2020-03-30 16:00:00 -0400
categories: devlog
tags: spring devlog code check
---

## @Autowired 지양

Spring Framework에 종속적 제거 , 불변성 유지를 위해 지양

```java
public class RestSalesController {
    private final SalesService salesService;

    public RestSalesController(SalesService salesService) {
        this.salesService = salesService;
    }   
}
```

생성자의 인자가 많아지는 경우 final을 받는 파라미터를 생성자로 만들어주는 @RequiredArgsConstructor를 사용해도 됨.

단, 이때는 인자의 추가나 순서 변경시 생성자 클래스가 변경되는 점에 주의해야함.

```java
@RequiredArgsConstructor
public class RestSalesController {
    private final SalesService salesService;
}
```

## DTO 잘 사용하기

DTO는 사용에 따라 최대한 쪼개야한다.

Entity를 용도에 따라 보여주는 부분이 다를 때, 각각의 목적에 따라 DTO를 만들어야 한다.

DTO는 용도와 레벨에 맞는 곳에 위치해야 한다. Controller까지, Service단 까지 등 용도와 레벨에 맞게 위치 시켜야 한다.






# 참고 문서
https://cheese10yun.github.io/lombok/