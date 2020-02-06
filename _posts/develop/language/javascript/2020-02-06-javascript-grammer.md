---
title: '[JavaScript] 문법'
date: 2020-02-06 17:01:00 -0400
categories: devlog
tags: javascript devlog function
---

## Destructuring assignment (구조 분해 할당)

### 구조 분해

좌측 :값을 넣을 변수

우측 : 값이되는 변수

```javascript
var a, b, rest;
[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2

[a, b, ...rest] = [1, 2, 3, 4, 5];
console.log(a); // 1
console.log(b); // 2
console.log(rest); // [3, 4, 5]

({ a, b } = { a: 1, b: 2 });
console.log(a); // 1
console.log(b); // 2
```

### 배열 구조 분해

```javascript
const foo = ['one', 'two', 'three'];
const [one, two, three] = foo;

console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
```
