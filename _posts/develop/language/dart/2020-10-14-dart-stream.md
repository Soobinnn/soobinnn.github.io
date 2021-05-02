---
title: '[Dart] Stream'
date: 2020-10-14 02:13:00 -0400
categories: devlog
tags: dart devlog stream
---

# Stream

스트림은 데이터나 이벤트가 들어오는 통로

비동기 작업을 할 때 주로 쓰인다.

네트워크에서 데이터를 받아서 UI에 보여주는 상황에 데이터를 만드는 곳과 소비하는 곳을 따로 둬서 문제를 해결함.

스트림이란 데이터의 추가나 변경이 일어나면 이를 관찰하던데서 처리하는 방법 (옵져버 패턴)

## Future와 다른 점은?

Dart의 비동기 프로그래밍은 Future 및 Stream 클래스로 주로 처리함.

Future는 즉시 완료되지 않는 계산을 나타냄.
일반 함수가 결과를 반환하는 경우 비동기 함수는 Future를 반환하며, 결과에 포함됨. 결과가 준비되면 Future에 알려주는 것.

Stream은 일련 비동기 이벤트임.

요청 시 다음 이벤트를 받는 대신 스트림이 준비되면 이벤트가 있음을 알려주는 비동기 Iterable과 같음.

## 스트림 이벤트 수신

스트림은 여러 가지 방법으로 만들 수 있다.

비동기 for 루프 (await for)는 for 루프 반복과 같은 스트림 이벤트를 반복함.

```dart
Future<int> sumStream(Stream<int> stream) async {
    var sum = [];
    await for (var value in stream) {
        sum += value;
    }
    return sum;
}
```

```dart

Stream<int> countStream(int to) async* {
    for(int i= 1; i<=to; i++) {
        yield i;
    }
}
```

```dart
main() async {
    var stream = countStream(10);
    var sum = await sumStream(stream);
}
```

## 오류 이벤트

await for를 사용하여 스트림을 읽을 떄 루프 문에 의해 오류가 발생함.

이것도 루프를 종료함. try-catch를 사용해 오류를 잡을 수 있다.

```dart
Future<int> sumStream(Stream<int> stream) async {
  var sum = 0;
  try {
    await for (var value in stream) {
      sum += value;
    }
  } catch (e) {
    return -1;
  }
  return sum;
}
```