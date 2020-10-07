---
title: '[Flutter] Navigation'
date: 2020-10-06 17:00:00 -0400
categories: devlog
tags: devlog flutter navigation
---

## 새로운 화면으로 이동

### push로 새로운 화면 호출

FirstPage 클래스를 수정하여 SecondPage로 전환하려면 navigator 클래스의 push() 메서드를 사용함.

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => [이동할 페이지]),
);
```

첫번째 인수로 context가 필요하고, 두번쨰 인수로 MaterialPageRoute 인스턴스가 필요함.

이 클래스는 머터리얼 디자인으로 작성된 페이지 사이에 화면 전환을 할 때 사용됨.

이 클래스의 builder 프로퍼티에 이동할 페이지를 나타내는 함수를 작성함.

### pop으로 이전 화면으로 이동

```dart
onPressed: () {
  Navitgator.pop(context),
}
```

### 새로운 화면에 값 전달하기

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondPage(person: person)),
)
```

### 이전화면으로 데이터 돌려주기

```dart
Navigator.pop(context, 'ok')
```

```dart
onPressed: () async {
  final person = Person('홍길동',20);
  final result = awaitNavigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondPage(person: person)),
  )
}
```

push() 메서드는 Future 타입의 변환 타입을 가집니다. Future는 미래에 값이 들어올 것을 나타내는 클래스. Future값을 반환받으려면 다음 두가지 조치를 해야함.

await키워드를 메서드 실행 앞에 추가하고, 메서드의 인수와 함수 본문 사이에 async키워드를 추가한다.

### Routes를 활용한 네비게이션

#### Routes 정의

MaterialApp 클래스의 routes 프로퍼티에 다음과 같은 형태로 정의할 수 있다.

```dart
return MaterialApp(
  title: 'Flutter Demo',
  theme: ThemeData(
    primarySwatch: Colors.blue,
  ),
  home: FirstPage(),
  routes: {
    '/first': (context) => FirstPage(),
    '/second': (context) => SecondPage(),
  }
)
```

#### 화면 이동

```dart
onPressed: () async {
  final result = await Navigator.pushNamed(context, '/second');
}
```

### 네비게이션 동작 방식의 이해

#### StatelessWidget 클래스 동작

#### StatefulWiget 클래스 동작

StatefulWidget 클래스의 build() 메서드에서는 앱성능에 지장을 줄만한 코드는 작성하면 안됨.

#### initState, dispose

StatefulWidget 클래스에는 build() 메서드 외에도 특정 타이밍에 실행되는 여러 메서드가 있다.

이러한 메서드들을 생명주기메서드라고 부른다.

initState() 메서드는 위젯이 생성될 떄 호출됨.

dispose() : 위젯이 완전히 종료될 때(pop) 호출됨

\*\* build() 메서드에서 복잡한 처리나 네트워크 요청등을 하면 안됨

-> initState() 메서드에서 수행해야함.
