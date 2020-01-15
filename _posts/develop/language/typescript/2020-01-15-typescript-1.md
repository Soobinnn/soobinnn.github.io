---
title: '[TypeScript] What is TypeScript'
date: 2020-01-15 15:13:00 -0400
categories: devlog
tags: typescript devlog
---

# TypeScript 란?

마이크로소프트에서 개발한 자바스크립트(ES6) Superset 언어

자바스크립트 문법을 그대로 사용하면서 타입을 추가하여 엄격하게 문법을 체크함.

## 장점

- 쉬운 도입

  > 모든 자바스크립트 코드는 타입스크립트 코드

- 정적 타입
  > 컴파일 타임 타입 체크

> IDE에서 실시간으로 에러를 발견하고 고칠 수 있음

- 자동완성 기능
  > 사용할 수 있는 함수, 변수 제안

> 타이핑 줄고 생산성 좋아짐

- 안전한 리팩토링
  > 함수 이름이나 변수명을 쉽게 바꿀 수 있음

> 더 이상 전체 파일 검색 안 해도 됨

- 새로운 문법 사용
  > ES6/ESNext 문법 대부분 지원

> Optional chaining, Nullish coalescing operator

- 거대한 커뮤니티

## 고려사항

1. 레거시 자바스크립트 코드랑 같이 사용하기 어려움

2. 복잡한 설정<br/> babel, webpack, awesome-typescript-loader, ts-loader, ts-node, d.ts, tsconfig 등 알아야함.

3. 관련 테스트 프레임워크, 정적분석도구도 타입스크립트를 지원해야 함.

## 예제

```typescript
function greeter(person: string) {
  return 'Hello, ' + person;
}
```

# 참고 문서

https://subicura.com/2020/01/07/2019-dev-summary.html
