---
title: "[JavaScript] Call Stack"
date: 2020-03-26 11:43:00 -0400
categories: devlog
tags: javascript devlog callstack
---

#  Call Stack

Javascript는 단일 스레드, 단일 동시 언어이므로 한번에 하나의 작업, 한번에 코드를 처리 할 수 있다.

단일 호출 스택으로, Heap과 같은 다른부분과 함께 Queue가
Javascript Concurrency Model(V8)을 구성함.

## 구조
![image](/assets/img/post/javascript/javascript-call-stack-01.png)

- 1. Call Stack
- 2. Heap
- 3. Queue

## 1. Call Stack

기본적으로 프로그램의 위치에 따라 함수 호출을 기록하는 데이터구조


## 2. Heap

객체는 힙에 할당됨.

대부분 구조화되지 않은 메모리 영역. 변수 및 객쳉 ㅔ대한 모든 메모리 할당이 여기서 발생함.

## 3. Queue

Javascript 런타임에는 처리 할 메시지 목록과 실행할 콜백 함수 목록인 메시지 큐가 포함됨.

스택의 용량이 충분하면 메시지가 대기열에서 꺼내어 관련 함수를 호출하여 초기 스택 프레임을 만드는 메시지로 처리됨.

스택이 다시 비워지면 메시지 처리가 종료됨.

이 메시지는 콜백 함수가 제공된 경우 외부 비동기 이벤트에 대한 응답으로 대기함.

예를 들어 사용자가 버튼을 클릭하고 콜백 기능이 제공되지 않은 경우 메시지가 대기열에 포함되지 않음.


# Event Loop




# 참고 문서
https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec