---
title: '[test] What is Static Analysis ?'
date: 2020-01-03 19:30:00 -0400
categories: sre
tags: test sre 정적분석 static-analysis
---

# 정적분석이란?

실제 실행 없이 코드를 분석.

(실행 중인 프로그램을 분석하는 것을 동적 프로그램 분석이라 함.)

\*\* 헬스할 때 운동 자세가 중요해서 자세를 교정하듯이, 프로그래밍의 자세를 올바르게 하기 위해 필요하다.

## 동적 테스트가 발견하지 못하는 버그

버그의 이유는 많지만 크게 4가지로 구분함.

1. 고려하지 못한 케이스 (요구사항 누락)
2. 기대하지 않은 동작 (요구사항 오해)
3. 예상치 못한 입력 (예외 처리에 대한 누락)
4. 단순한 코딩 실수로 인한 버그

1, 2번은 동적 테스트로 어느 정도 커버가 가능하다. 잘 정리된 요구사항과 100%의 커버리지, QA 프로세스로 대부분의 버그를 잡아낼 수 있다.

### 3.예상치 못한 입력

대표적인 예로 divide by zero, buffer overrun과 같은 버그

### 4. 단순한 코딩 실수로 인한 오동작

대표적인 예로 memory leak

오랜 시간 동작하면서 차곡차곡 쌓아져야만 문제가 드러난다.

개발 단계에서 빨리 결과를 확인해야 하는 동적 테스트에서는 발견하기가 쉽지않다. memory leak 같은 경우 해당 버그가 발견되었음에도 어느부분에서 leak이 발생하는 지 찾아내기도 힘들다.

## 정적 분석이 필요한 경우

정적 분석은 경험 많은 개발자들의 노하우나 여러 실행 시간 오류들의 사례로 부터 규칙을 만든다. 그리고 만들어진 규칙을 사용하여 소스 코드 전반에 걸쳐 분석을 수행한다.

1. 적은 비용으로 경험 많은 개발자의 활동을 대체하는 방법<br> 실행 시간 오류 같은 버그를 적은 노력으로 미연에 방지 할 수있다.

2. 미처 예상하지 못한 입력이나 프로그램의 흐름 혹은 리뷰에서 실수로 빼먹은 코드에 대해서도 검사를 수행하여 동적 테스트나 코드 리뷰 같은 활동으로 잡지 못하는 버그도 찾을 수 있다.

3. 코드의 실행이 필요 없다. 완성되지 않은 코드에 대해서도 분석이 가능하기 때문에 동적 테스트보다 이른 시점에 버그를 찾아낼 수 있다.

4. 동적 테스트보다 비교적 적은 시간에 버그를 찾아낼 수 있다.

5. 버그 뿐만 아니라 개선의 여지가 있는 코드들도 찾아준다. (코딩 스타일 가이드, 코드의 품질 메트릭도 제공)

## 동적 테스팅 vs 정적 테스팅

동적 테스트는 테스트 방법 중에서도 비용이 많이 드는 작업이다.

소스 코드가 늘어나고 복잡해 짐에 따라 유지보수 해야 하는 테스트 코드의 양도 같이 증가한다.

또한 테스트 코드 역시 코딩 과정이므로 당연히 실수가 발생하고 테스트 코드의 실수는 품질에 큰 영향을 미친다.

## 정적 분석 툴 종류

1. PMD
2. FindBugs
3. CheckStyle
4. Sonarqube

### PMD

미사용 변수, 비어있는 코드 블락, 불필요한 오브젝트 생성과 같은 Defect을 유발할 수 있는 코드를 검사

https://pmd.github.io

### FindBugs

정해진 규칙에 의해 잠재적인 에러 타입을 찾아줌

http://findbugs.sourceforge.net

### CheckStyle

정해진 코드 룰을 잘 따르고 잇는지에 대한 분석

http://checkstyle.sourceforge.net

### SonarQube

코드를 수정하는과 동시에 자동으로 분석을 하고 리포팅까지 해줌
