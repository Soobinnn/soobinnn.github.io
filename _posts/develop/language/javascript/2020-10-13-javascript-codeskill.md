---
title: '[JavaScript] Code Skill'
date: 2020-10-13 15:31:00 -0400
categories: devlog
tags: javascript devlog code skill
---

## 배열

### 두개 배열이 있을 때

```javascript
let arr1 = [1, 2, 3];
let arr2 = [2, 3, 4, 5];
```

1. 차집합

```javascript
let difference = arr1.filter((x) => !arr2.includes(x)); // 결과 1
```

2. 교집합

```javascript
let difference = arr1.filter((x) => arr2.includes(x)); // 결과 2, 3
```

3. 배타적 논리합

```
let difference = arr1.filter(x => !arr2.includes(x)).concat(arr2.filter(x => !arr1.includes(x)));
```
