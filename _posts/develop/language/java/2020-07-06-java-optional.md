---
title: '[Java] Optional'
date: 2020-07-06 09:21:00 -0400
categories: devlog
tags: laravel devlog java optional
---

## null 반환 문제점

메소드에서 null을 반환한다면, 해당 메소드를 사용하는 여러 곳에서 문제점이 발생할 수 있음.

- NPE (NullPointerException)을 발생시킬 위험이 있다.
- NPE (NullPointerException)방어를 위한 null 체크 로직이 필요하다
- null 체크 로직 때문에 코드 가독성이 떨어진다. -> unll 체크 로직은 코드 가독성을 떨어지게 하고, 프로그래머의 생산성 저하.

## 해결 방법

null을 반환하는 대신 Optional을 활용

# Optional ?

java8 부터 제공하는 null을 포함하거나 null을 포함하지 않을 수도 있는 객체

## 장점

- NPE (NullPointerExcetpion)을 발생시킬 수 있는 null을 직접 다루지 않아도 된다.

- null 체크 로직이 필요 없다
- 명시적으로 해당 변수가 null일 가능성을 표현할 수 있다.

### example

#### Before

```java
public static Integer findMinMultiple(List<Integer> numbers, int anyNumber) {
    Collections.sort(numbers);
    for (Integer number : numbers) {
        if (number % anyNumber == 0) {
            return number;
        }
    }
    return null;
}
```

#### After

```java
public static OptionalInt findMinMultiple(List<Integer> numbers, int anyNumber) {
    Collections.sort(numbers);
    for (Integer number : numbers) {
        if (number % anyNumber == 0) {
            return OptionalInt.of(number);;
        }
    }
    return OptionalInt.empty();
}
```

```java
public static OptionalInt findMinMultiple(List<Integer> numbers, int anyNumber) {
    return numbers.stream()
        .sorted()
        .filter(number -> number % anyNumber == 0)
        .findFirst()
        .map(OptionalInt::of)
        .orElseGet(OptionalInt::empty);
}
```

## 결론

예외를 던지는 것은 정말 예외적인 상황에서만 사용해야 한다. -> 예외 생성시, 스택 추적 전체를 캡처하므로 비용이 만만치 않음.

진짜 예외적인 상황이 아니라면 Optional을 반환하는 것이 좋다.

**하지만 Optional은 신중히 사용해야 한다.**

Optional은 값을 포장하고 다시 풀고, 값이 없을 때 대체하는 값을 넣는 등의 오버헤드가 있으므로, 무분별하게, 적절하지 않게 사용된다면 성능 저하가 뒤따르기 때문이다.

적절하지 않게 사용되는 예로 Optional의 orElse 메소드가 있다.

orElse(...)에서의 값은 Optional에 값이 있든 없든 무조건 실행된다. Optional에 값이 있다면 orElse의 인자로서 실행된 값은 무시되고 버려진다.

따라서 이미 생성되었거나 계산된 값이 아니라면 orElseGet메소드를 쓰는 것이 적절하다.

## Optional 사용 시 주의 사항

array / list를 리턴하는 것에는 절대 사용해서는 안된다. -> 대신 빈배열 또는 목록을 리턴.

필드, 메소드 파라미터로 사용해서는 안됨.

Getter에 대한 반환 값으로 일상적으로 사용하는 것은 과용.

# 참고 자료

https://woowacourse.github.io/javable/2020-04-21/optional-vs-null

[공식문서](https://docs.oracle.com/javase/9/docs/api/java/util/Optional.html)

[Optional 만든 의도](https://stackoverflow.com/questions/26327957/should-java-8-getters-return-optional-type/26328555#26328555)

[Optional을 올바르게 사용하는 것이 선택이 아닌 26가지 이유](https://dzone.com/articles/using-optional-correctly-is-not-optional)

http://www.yes24.com/Product/Goods/65551284

http://homoefficio.github.io/2019/10/03/Java-Optional-%EB%B0%94%EB%A5%B4%EA%B2%8C-%EC%93%B0%EA%B8%B0/
