---
title: '[React] Flux Architecture'
date: 2020-03-19 23:10:00 -0400
categories: devlog
tags: react devlog flux
---

# Flux

단방향

불변성을 유지하기 위해 Reducer패턴을 사용해서 기존의 데이터에 대한 수정 없이 새로운 데이터를 반환하기 위해 reducer라는 개념을 적용한다.

데이터의 단방향성이 가능한 이유
: reducer를 이용한 데이터의 불변성

Flux의 구현체 reducer

# 구조

// 그림

- Action

- Store

- Reducers

# Get Starting
```
npm i redux --save
yarn add redux
```