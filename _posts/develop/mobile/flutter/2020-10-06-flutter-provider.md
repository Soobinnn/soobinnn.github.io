---
title: '[Flutter] Provider'
date: 2020-10-06 14:00:00 -0400
categories: devlog
tags: devlog flutter provider
---

## dependencies 추가

```
provider
```

Provider 패키지에서 제공하는 주요 클래스는 다음과 같다.

- ChangeNotifierProvider
- MultiProvider
- Provider
- Consumer

ChageNotifierProvider 클래스는 단일 모델을 제공하는 역할을 함. 만약 다수 모델 클래스를 지정하려면 MultiProvider 클래스를 사용함.

Provider는 앞서 지정한 모델에 접근하여 값을 갱신할 수 있도록 해줌. Consumer 클래스는 Provider 클래스에 제공되는 모델 클래스를 읽어오는 클래스 Provider가 변경되면 Consumer로 감싼 위젯은 자동으로 갱신됨.

### setting

```dart
void main() => runApp(
  ChangeNotifierProvider(
    builder: (context) => SimpleState(),
    child: StateLoginDemo(),
  )
);
```
