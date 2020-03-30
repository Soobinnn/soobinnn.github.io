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

## final

변수 -> 해당 변수의 값은 변경이 불가능해짐. 상수

변수의 참조 -> 참조 변수가 Heap 내의 다른 객체를 가리키도록 변경할 수 없다.

메소드 -> 해당 메소드를 상속받는 하위 클래스에서 오버라이딩을 할 수 없다. (상속받는 하위 클래스에서도 변경이 되지 않아야 하는 메소드의 경우 사용)

클래스 -> 해당 클래스를 다른 클래스가 상속받을 수 없다.


## finally

try-catch 블록 뒤에 둘 수 있는 선택적 블록.

try-catch문이 끝나기 전에 항상 꼭 실행되어야하는 로직이 있을 경우 finally절에 둔다.

try-catch블록과 함께 사용되며 예외가 던져지더라도 항상 실행될 코드를 지정하기 위해 사용된다.

try, catch블록이 전부 실행된 후 , 제어 흐름이 원래 지점으로 돌아가기 전에 실행된다.
즉, 보통 뒷 마무리 코드를 작성하는데 사용된다.

\* try블록 안에 return문을 넣어도 실행되는가?
fianlly가 실행 된 다음에서야 return이 이뤄진다.
try블럭에서 return, continue, break 문이 실행하거나, 예외를 던진다거나해도 실행된다.


## finalize

finalize 메소드는 java garbage collector가 더 이상 참조가 존재하지 않는 객체를 발견한 순간 호출하는 메소드.

더 이상 사용되지 않는 객체가 있을 때 메모리 낭비를 막기 위해서 garbage collector가 이 객체를 없애버리는데 이 때 해당 객체의 finalize 메서드를 호출해서 없앤다.

finallize()는 java.lang.Object 클래스로 부터 상속받아 모든 클래스의 객체가 가지고 있는 메소드다. 

만약 객체가 삭제되기 직전에 실행되어야 하는 로직이 있으면 Object클래스에 정의된 finalize()
메소드를 오버라이딩하여 정의할 수 있다.

finalize()는 언제 호출될지 알 수 없기 때문에, finalize()를 오버라이딩 했다고해서 여기에 의존하는 방식의 코딩은 좋은 방법은 아닐 수 있다.
