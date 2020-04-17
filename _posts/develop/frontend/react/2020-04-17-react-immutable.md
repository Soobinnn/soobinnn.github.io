---
title: '[React] Immutable'
date: 2020-03-19 23:10:00 -0400
categories: devlog
tags: react devlog immutable
---

# Immutable

## 사용하는 이유

자바스크립트에서 primitive data type은 변경 불가능 한값이며,

primitive data type 이외의 모든 값(객체)는 변경 가능한 값이다.

immutable를 쓰는 이유는 성능 때문이다.

mutable value는 값에 대한 메모리 주소를 참조하기 때문에 값을 변경했을 경우 
해당 값을 사용하고 있는 모든 곳에서 side effect가 발생하여 예상치 못한 버그를 유발 할 수 있다.

immutable로 객체를 선언하고 사용하게 되면 객체의 메모리 주소가 불변하기 때문에 구조를 단순하게 유지할 수 있고 

그로 인해 구조적인 공유를 할 수 있어 애플리케이션을 추론하기 쉽게 된다.

내부적으로 구조를 공유하고 있기 때문에 메모리 사용량을 획기적으로 감소시키는 장점도 가지게된다.

객체를 immutable로 선언할 때는 Object.freeze 메소드를 사용하면 되는데,

Object.freeze 메소드 객체 안에 있는 nested object까지 immutable로 지정하는 건 아니기 때문에, nested object가 바뀌는 것 까지 막지 못하므로 주의해야함.


다중 스레드 환경에서 안전하다

방어적 복사본을 만들 필요가 없다.

## 규칙
객체는 Map
배열은 List
설정할땐 set
읽을땐 get
읽은다음에 설정 할 땐 update
내부에 있는걸 ~ 할땐 뒤에 In 을 붙인다: setIn, getIn, updateIn
일반 자바스크립트 객체로 변환 할 땐 toJS
List 엔 배열 내장함수와 비슷한 함수들이 있다 – push, slice, filter, sort, concat… 전부 불변함을 유지함
특정 key 를 지울때 (혹은 List 에서 원소를 지울 때) delete 


## 참고 자료
https://galid1.tistory.com/622