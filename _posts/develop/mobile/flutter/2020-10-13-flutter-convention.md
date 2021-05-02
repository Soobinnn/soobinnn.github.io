---
title: '[Flutter] Effective-dart Convention'
date: 2020-10-13 01:25:00 -0400
categories: devlog
tags: devlog flutter convention effective-dart
---

# 참고 문서
pubspec.yaml 파일에 dev_dependencies 안에 `effective_dart` 추가
```
dev_dependencies:
  effective_dart: ^1.2.0
```

pubspec.yaml가 있는 동일한 depth 디렉토리에 analysis_options.yaml 파일 추가

analysis_options.yaml파일 안에 아래 내용 추가
```
include: package:effective_dart/analysis_options.yaml 추가
```

https://velog.io/@adbr/flutter-flutter-linter-package-effectivedart#%EC%9D%B4%EB%B2%88-%ED%95%9C%EB%B2%88%EB%A7%8C-%EC%A1%B0%EC%9A%A9%F0%9F%A4%AB

https://pub.dev/packages/effective_dart