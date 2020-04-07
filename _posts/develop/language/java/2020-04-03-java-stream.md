---
title: '[Java] Stream'
date: 2020-04-03 09:41:00 -0400
categories: devlog
tags: java devlog date
---

# Stream API

Java 8에서 추가된 기능으로, stream 형태의 요소에 함수형 연산자를 지원해주는 클래스

## Stream
Array, Collections와 같이 연속된 형태의 객체이다. 하지만 자료구조는 아니다. 

위와 같은 데이터를 입력으로 받아 메소드로 처리할 뿐이다.

stream은 입력받은 원래의 자료구조를 바꾸지는 못한다. 대신, 파이프라인 형태로 연결된 메소드의 결과를 제공한다. 원본 데이터를 바꾸지 못하는 특성 덕분에 side effect를 제거할 수 있다.

최종 연산자(terminal operation)는 stream의 끝을 의미하며 모든 연산자를 수행한 결과를 반환한다. 다시말해, 최종 연산자까지 모두 수행한 stream은 재활용 할 수 없다.

```java
// 스트림 생성 -> 중간 연산자 -> 최종 연산자
int result = list.stream()  // 스트림 생성
        .filter( ... )      // 중간 연산자
        .map( ... )         // 중간 연산자
        .count();           // 최종 연산자
```

## 연산자

- Arrays.stream()
```java
String[] arr = new String[] {"Hello", "World", "Hell"};
Stream<String> stream = Arrays.stream(arr); // 배열
Stream<String> streamOfArrayPart = Arrays.stream(arr, 1, 3); // 부분 배열
```

- Collections.stream()
컬렉션 타입 (Collection, List, Set)은 메소드를 이용하여 스트림을 생성할 수 있다.
```java
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();
Stream<String> parallelStream = list.parallelStream(); // 병렬 처리 스트림
```
- 직접 생성하는 연산자

  - empty()

  null대신 이용할 수 있다.
  ```java
  Stream stream = Stream.empty();
  ```

  - build()

  ```java
  Stream<String> generatedStream = Stream.<String>builder()
        .add("Hello")
        .add("World")
        .build();
  ```

  - generate()
  
  크기를 지정하지 않으면 무한하기 때문에 특정 사이즈만큼 생성하려면 반드시 limit을통해 최대 크기를 제한해야 한다.
  ```java
  Stream<String> generatedStream = Stream.generate(() -> "gen").limit(5);
  ```

  - iterate()
  초기 값을 시작으로 계속해서 2씩 증가된 값을 생성한다. generate()와 마찬가지로 크기를 지정하지 않으면 무한하기 때문에 limit을 통해 크기를 제한해야 한다.

  ```java
  Stream<Integer> iteratedStream = Stream.iterate(30, n -> n + 2).limit(5);
  ```

- 기본 타입형 스트림

intStream, LongStream, DoubleStream

제너릭을 사용하지 않고 기본 값을 생성하는 방법.
제너릭을 사용하지 않기 때문에 불필요한 auto-boxing이 발생하지 않는다.

\* range는 [startPosition, endPosition) 범위를 가진다.
\* rangeClosed는 [startPosition, endPosition] 범위를 가진다.

```java
IntStream intStream = IntStream.range(1, 5); // [1, 2, 3, 4]
LongStream longStream = LongStream.rangeClosed(1, 5); // [1, 2, 3, 4, 5]
```

필요한 경우 boxed 메서드를 통해 Integer 형태로 박싱할 수 있다.
```java
Stream<Integer> boxedIntStream = IntStream.range(1, 5).boxed();
```

난수 스트림을 생성할 수도 있다.
```java
DoubleStream doubles = new Random().doubles(3); // 난수 3개 생성
```

# 참고 문서
https://velog.io/@kskim/Java-Stream-API