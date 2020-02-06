---
title: '[React] Redux Setting'
date: 2020-02-06 16:06:00 -0400
categories: devlog
tags: react devlog redux
header-img: '/img/logo/redux-logo.png'
---

# Redux Setting

1. Install
2. Module 생성
3. combineReducers로 루트 리듀서 생성
4. Store 생성
5. Provider를 사용하여 리액트 프로젝트에 스토어 연동
6. Connect함수를 사용하여 컴포넌트에 스토어 연동

## 1. Install

```
yarn add redux react-redux redux-action
```

## 2. Module 생성

- 액션 타입 정의
- 액션 생섬함수 정의
- 초기상태와 리듀서 정의

## 3. combineReducers로 루트 리듀서 생성

```javascript
import { combineReducers } from 'redux';
import 모듈1 from './~~';

// redux의 내장함수인 combineReducers로 리듀서를 하나로 합치는 작업을 함.
// 여러개로 나뉘어진 리듀서 : 서브리듀서
// 하나로 합쳐진 리듀서 : 루트 리듀서
export default combineReducers({
	모듈1
});
```

## 4. Store 생성

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { createStore } from 'redux';
import rootReducer from './store/modules';

const store = createStore(rootReducer);

ReactDOM.render(<App />, document.getElementById('root'));

serviceWorker.unregister();
```

## 5. Provider를 사용하여 리액트 프로젝트에 스토어 연동

리액트 프로젝트에 스토어를 연동 할 때에는 react-redux 라이브러리 안에 들어있는 Provider 라는 컴포넌트를 사용합니다. 기존의 JSX 를 Provider 로 감싸고, store 는 props 로 Provider한테 넣어줌.

## 6. Connect함수를 사용하여 컴포넌트에 스토어 연동

리덕스 스토어 안에 있는 값이나 액션 함수들을 연동해줄 것이다. 리덕스와 연동된 컴포넌트 -> 컨테이너 컴포넌트라 부름. 단순히 props를 전달해주면 그대로 보여주는 컴포넌트들 -> 프리젠테이셔널 컴포넌트라 부름.

\* 프리젠테이셔널 컴포넌트와 컨테이너 컴포넌트 이렇게 컴포넌트를 분류하는 방식은 리덕스 창시자가 제시한 방법 -> 권장하지맍 무조건 따를필요는 없음.

장점 : 프리젠테이셔널 컴포넌트 -> UI의 모야새에만 집중할 수 있음. 컨테이너 컴포넌트 쪽에서는 유저 인터렉션쪽에 집중 할 수 있다.

컨테이너 컴포넌트를 만들떄 react-redux안에 들어있는 `connect`라는 함수를 사용함.

함수의 파라미터에 전달해주는 `mapStateToProps`는 스토어 안에 들어있는 props로 전달해주고, `mapDispatchToProps`는 액션 생성함수들을 props로 전달해줌

## Redux sub library

리덕스를 간편하게 사용하기 위한 라이브러리들

- redux-actions
- immer

### redux-actions

redux 액션 생성, 초기화, 리덕스 정의를 가독성 있게 해주는 라이브러리

`createAction` 이라는 함수를 사용

FSA 규칙을 따르는 액션 객체를 만들어 줘야함.

#### install

```
yarn add redux-actions
```

#### FSA 규칙

##### 필수 규칙

- 순수 자바스크립트 객체
- type 값이 있어야함

##### 선택 규칙

- error 값이 있음
- payload 값이 있음
- meta 값이 있음

FSA규칙을 따르는 액션 객체는 액션에서 사용할 파라미터의 필드명을 payload로 통일 시킴.

이를 통해 액션 생성 함수를 훨씬 더 쉽게 작성할 수 있음.

#### 액션 생성함수 예제

##### 1. FSA 규칙을 따르는 액션 생성 함수 정의

```javascript
const CHANGE_INPUT = 'waiting/CHANGE_INPUT'; // 인풋 값 변경
const CREATE = 'waiting/CREATE'; // 명단에 이름 추가
const ENTER = 'waiting/ENTER'; // 입장
const LEAVE = 'waiting/LEAVE'; // 나감
export const changeInput = text => ({ type: CHANGE_INPUT, payload: text });
export const create = text => ({ type: CREATE, payload: text });
export const enter = id => ({ type: ENTER, payload: id });
export const leave = id => ({ type: LEAVE, payload: id });
```

##### 2. createAction 으로 액션 만들기

```javascript
import { createAction } from 'redux-actions';

const CHANGE_INPUT = 'waiting/CHANGE_INPUT'; // 인풋 값 변경
const CREATE = 'waiting/CREATE'; // 명단에 이름 추가
const ENTER = 'waiting/ENTER'; // 입장
const LEAVE = 'waiting/LEAVE'; // 나감

// **** createAction 으로 액션 만들기
export const changeInput = createAction(CHANGE_INPUT, text => text);
export const create = createAction(CREATE, text => text);
export const enter = createAction(ENTER, id => id);
export const leave = createAction(LEAVE, id => id);
```

결론 : createAcition 사용할 시 가독성이 좋아짐.

#### createAction

createAction 함수에서 두번째 파라미터로 받는 부분은 payloadCreator로서, payload를 어떻게 정할지 설정함.

만약에 생략하면 기본적으로 payload => payload 형태로 되기 때문에, 위 코드를 다음과 같이 작성해도 작동에 있어서 차이가 없음.

대신 두번째 파라미터를 생략한다면, 해당 액션에서 어떤 값을 payload로 설정했는지 헷갈릴 가능성이 있음.

현재 상황에서는 데이터를 새로 생성 할 때마다 고유 id값을 주어야 하는데, 변화를 일으키는 함수, 리듀서는 순수한 함수여야함.

데이터에 고유 id를 주는 작업은 리듀서에서 발생하면 안되고, 액션이 스토어에 디스패치 되기 전에 이뤄져야 함.

```javascript
import { createAction, handleActions } from 'redux-actions';

const CHANGE_INPUT = 'waiting/CHANGE_INPUT'; // 인풋 값 변경
const CREATE = 'waiting/CREATE'; // 명단에 이름 추가
const ENTER = 'waiting/ENTER'; // 입장
const LEAVE = 'waiting/LEAVE'; // 나감

let id = 3;
// createAction 으로 액션 생성함수 정의
export const changeInput = createAction(CHANGE_INPUT, text => text);
export const create = createAction(CREATE, text => ({ text, id: id++ }));
export const enter = createAction(ENTER, id => id);
export const leave = createAction(LEAVE, id => id);

export default handleActions({});
```

#### handleActions

초기 상태와 리듀서 정의

handleActions을 사용하면 더이상 switch/case문을 사용할 필요 없이 각 액션 타입마다 업데이터 함수를 구현하는 방식으로 할 수 있어서 가독성이 더 좋아짐.

CREATE, ENTER, LEAVE의 액션 경우엔 배열을 다뤄야 하는 것들이라, concat, map, filter를 사용하여 불변성을 유지하면서 배열에 새로운 값을 지정해줌.

### Immer

불변성을 유지해줘야 하는 객체의 값을 더 쉽게 업데이트 할 수 있게 해줍니다.

#### Install

```
yarn add immutable
```

# 참고 문서

https://velog.io/@velopert/Redux-3-%EB%A6%AC%EB%8D%95%EC%8A%A4%EB%A5%BC-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%99%80-%ED%95%A8%EA%BB%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-nvjltahf5e

https://velog.io/@velopert/20180908-1909-%EC%9E%91%EC%84%B1%EB%90%A8-etjltaigd1
