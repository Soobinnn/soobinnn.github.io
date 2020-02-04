---
title: '[React] Redux'
date: 2020-02-04 12:29:00 -0400
categories: devlog
tags: react devlog redux store
header-img: '/img/logo/redux-logo.png'
---

# Redux 란?

상태 관리 라이브러리 중 사용률이 높은 라이브러리

컴포넌트들의 상태 관련 로직들을 다른 파일들로 분리시켜서 더욱 효율적으로 관리

컴포넌트끼리 상태를 공유하게 될 때 여러 컴포넌트를 거치지 않고도 상태 값 전달 할 수 있음

리덕스의 미들웨어라는 기능을 통하여 비동기 작업, 로깅 등 확장적인 작업들을 더욱 쉽게 할 수도 있게 해줌.

\* 리덕스는 리액트에 종속되지 않는다. 리액트에서 사용하려고 만든거지만, 다른 UI 라이브러리나 프레임워크와 함께 사용 될 수 있다.

# 개념

- Action
- Action Creator
- Reducer
- Store
- Dispatch
- Subscribe

## Action

상태에 어떠한 변화가 필요하게 될 때, 액션이라는 것을 발생시킴.

하나의 객체로 표현됨.

```
{
  type: "TOGGLE_VALUE"
}
```

\* 액션 객체는 **type** 필드를 필수적으로 가지고 있어야함.

```
{
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}

{
  type: "CHANGE_INPUT",
  text: "test"
}
```

## Action Creator

액션을 만드는 함수.

단순히 파라미터를 받아와서 액션 객체 형태로 만들어줌

```

```

## Reducer

변화를 일으키는 함수

Reducer는 두가지 파라미터를 받아옴.

1. 현재 상태
2. 액션

새로운 상태를 만들어서 반환함.

```javascript
function reducer(state, action) {
	// 상태 업데이트 로직
	return alteredState;
}
```

## Store

리덕스에서는 한 애플리케이션 당 하나의 스토어를 만들게 된다.

스토어 안에는 현재 앱 상태와 리듀서가 들어가 있고 추가적으로 몇가지 내장함수들이 있다.

## Dispatch

스토어의 내장 함수 중 하나. 액션을 발생 시키는 것

dispatch라는 함수에서 액션 파라미터로 전달

Store는 리듀서 함수를 실행 시켜 해당 액션을 처리하는 로직이 있다면 액션을 참고하여 새로운 상태를 만들어줌.

## Subscribe

구독 또한 스토어의 내장함수 중 하나 subscribe함수는 함수 형태의 값을 파라미터로 받아옴.

함수 형태의 값을 파라미터로 받아옴.

subscribe함수에 특정 함수를 전달해주면, 액션이 디스패치 되었을 때 마다 전달해준 함수가 호출됨.

# 참고 문서

https://medium.com/@ca3rot/%EC%95%84%EB%A7%88-%EC%9D%B4%EA%B2%8C-%EC%A0%9C%EC%9D%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-%EC%89%AC%EC%9A%B8%EA%B1%B8%EC%9A%94-react-redux-%ED%94%8C%EB%A1%9C%EC%9A%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-1585e911a0a6

https://velog.io/@velopert/Redux-1-%EC%86%8C%EA%B0%9C-%EB%B0%8F-%EA%B0%9C%EB%85%90%EC%A0%95%EB%A6%AC-zxjlta8ywt
