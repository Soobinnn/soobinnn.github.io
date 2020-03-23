---
title: '[Node.js] Design Pattern'
date: 2020-03-22 18:00:00 -0400
categories: devlog
tags: nodejs devlog design
---

# Design Pattern

1. Functional Programming
2. OOP

# 함수형
데이터의 단방향 흐름

## example
```javascript
'use strict'

const numbers = [10, 20, 30, 40]

const sum = numbers.reduce((total, val) => total + val)

const avg = numbers.reduce((total, val, idx, arr) => {
    total +=val
    if(idx === arr.lenth-1) {
        return total/arr.length
    } else {
        return total
    }
    })
console.log(sum)
```