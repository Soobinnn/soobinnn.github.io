---
title: '[Dart] Dart Function'
date: 2020-05-01 02:42:00 -0400
categories: devlog
tags: dart devlog function
---

```dart
void main() {
    var test = "test";
    print('test = $test');
}
```

```dart
void printMsg(String msg, [String value = 'undefined']) {
    print('msg = $msg, value = $value');
}

void main() {
    printMsg('1234', '5678');
    
    printMsg('1234');
}

```