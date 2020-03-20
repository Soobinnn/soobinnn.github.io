---
title: "[JavaScript] 성능 비교"
date: 2020-03-19 11:26:00 -0400
categories: devlog
tags: javascript devlog
---
DOM이 다시 그리는 횟수를 줄여야 합니다. DOM은 element를 추가하고, 사이즈 변경, 위치등의 변경사항이 있을 때마다 다시 그리게 됩니다.
DOM의 변경으로 다시 렌더 트리를 재생성 하는 과정을 Reflow, 재생성된 렌더 트리를 다시 그리는걸 Repaint(or Redraw)라 합니다.
DOM이 변경될때마다 다시 그리게 되므로 이과정을 최소화 하여야 합니다.
이런 행위가 반복되면 속도가 느려지게 됩니다.

# 객체 생성, 초기화 성능

## Bad
생성자
```javascript
var arr = new Array();

```
## Good
리터럴 형식
```javascript
var arr = [];
```




# For문 비교
- for
- for in
- while
- do while

- forEach
- map
- filter
- reduce
- every/some
- includes
- indexOf
- find
- findIndex

for ... in 문은 객체의 모든 열거 가능한 속성을 반복합니다.
for ... of 문은 모든 객체가 아닌 컬랙션만 반복합니다. [Symbol.iterator] 속성이 있는 컬렉션의 프로퍼티를 반복합


TypeArray ?



for in은 prototype에 접근하여 기존의 정의된 메소드까지 포함하여 출력하므로 비효율적

# String
문자열길이가 짧을 땐 += 연산자가 빠르고
길땐 join이 우월하다.

* 참고
jsMatch

https://12bme.tistory.com/134

https://12bme.tistory.com/185?category=682905

https://joshua1988.github.io/web-development/javascript/javascript-best-practices/


https://trustyoo86.github.io/javascript/2019/08/27/js-optimization.html

https://ljlm0402.netlify.com/javascript/performance/