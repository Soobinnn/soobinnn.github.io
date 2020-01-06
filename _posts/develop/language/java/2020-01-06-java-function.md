---
title: '[Java] Java Function'
date: 2020-01-06 09:50:00 -0400
categories: devlog
tags: java devlog
---

## IntStream

Java8에서 추가된 메소드.

원시 데이터형 int를 스트림으로 다룰 수 있도록 해줌.

```java
//
IntStream.of(1,2,3,4,5)

//
IntStream.range(1,5);

//
IntStream.rangeClosed(1,5);
```

### iterator function

```java
// 0, 2, 4, 6에 대한 스트림 생성
IntStream.iterator(0, i -> i +2).limit(4);
```

### anyMatch function

```java
//1,2,3,4 중 짝수인 것이 하나라도 있으면 참
IntStream.range(1, 5).anyMatch(i -> i%2 ==0);
```

### allMatch function

```java
//1,2,3,4 모두 짝수면 참
IntStream.range(1, 5).allMatch(i -> i%2 ==0);
```

### noneMatch function

```java
//1,2,3,4 모두 짝수가 아니면 참
IntStream.range(1, 5).nonMatch(i -> i%2 ==0);
```

### filter function

```java
IntStream.range(1,5).filter(i-> i%2 == 1);
IntStream.range(1,5).filter(i-> i%2 == 1).allMatch(i -> i%2 == 1);
IntStream.range(1,5).filter(i-> i%2 == 1).nonMatch(i -> i%2 == 1);
```

### max/ min function

```java
IntStream.range(1,5).max().getAsint();
IntStream.range(1.5).min().getAsint();
```
