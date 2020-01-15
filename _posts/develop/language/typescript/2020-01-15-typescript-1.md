---
title: '[TypeScript] What is TypeScript'
date: 2020-01-15 15:13:00 -0400
categories: devlog
tags: typescript devlog
---

# TypeScript 란?

마이크로소프트에서 개발한 자바스크립트(ES6) Superset(상위 확장) 언어

자바스크립트 문법을 그대로 사용하면서 타입을 추가하여 엄격하게 문법을 체크함.

# 특징

![typescript_superset](/assets/img/post/typescript/typescript-superset.png)

## 장점

- 쉬운 도입

  > 모든 자바스크립트 코드는 타입스크립트 코드

- 정적 타입 언어

  > 컴파일 타임 타입 체크 (단, 전통적인 컴파일 언어와 다르게 링킹과정이 생략됨)

  > 암묵적 형변환, 호이스팅, 복잡성 문제 해결

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

### Compile / Intepreter

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

https://velog.io/@dongwon2/TypeScript%EB%A5%BC-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-%EC%9D%B4%EC%A0%95%EB%8F%84%EB%8A%94-%ED%95%B4%EC%A4%98%EC%95%BC%EC%A7%80
