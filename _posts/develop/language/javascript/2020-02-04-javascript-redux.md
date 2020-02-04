---
title: '[JavaScript] Redux Example-1'
date: 2020-02-04 18:00:00 -0400
categories: devlog
tags: javascript devlog redux store react
header-img: '/img/logo/redux-logo.png'
---

# JavaScript에서 Redux 사용하기

Redux는 리액트에 종속되지 않는다. 리액트에서 사용하려고 만든거긴 하지만, 실제로 다른 UI 라이브러리나 프레임워크와 함께 사용 될 수도 있다.

> Vailla JavaScript란?
>
> > 라이브러리나 프레임워크 없이 사용하는 자바스크립트 그 자체를 의미. 순수 자바스크립트

```javascript
import { createStore } from 'redux';

const lightDiv = document.getElementsByClassName('light')[0];
const switchButton = document.getElementById('switch-btn');

const counterHeadings = document.getElementsByTagName('h1')[0];
const plusButton = document.getElementById('plus-btn');
const minusButton = document.getElementById('minus-btn');

// 액션 타입 정의
const TOGGLE_SWITCH = 'TOGGLE_SWITCH';
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

// 액션 생성함수 정의
const toggleSwitch = () => ({ type: TOGGLE_SWITCH });
const increment = diff => ({ type: INCREMENT, diff });
const decrement = () => ({ type: DECREMENT });

// 초깃값 설정
const initialState = {
	light: false,
	counter: 0
};

// 리듀서 함수 정의
function reducer(state = initialState, action) {
	switch (action.type) {
		case TOGGLE_SWITCH:
			return {
				...state, // 기존의 값은 그대로 두면서
				light: !state.light // light 값 반전시키기
			};
		case INCREMENT:
			return {
				...state,
				counter: state.counter + action.diff
			};
		case DECREMENT:
			return {
				...state,
				counter: state.counter - 1
			};
		default:
			// 지원하지 않는 액션의 경우 상태 유지
			return state;
	}
}

// 리듀서 함수가 가장 처음 호출 될 떄는 state가 undefined 이다.
//  state가 undefined로 주어졌을 땐, initialState를 사용하도록 설정
// 리듀서에서는, 불변성을 유지해주면서 데이터에 변화를 일으켜주어야 합니다. 이러한 작업을 하기 위해서, ... spread 연산자를 사용하면 편합니다. 기존의 값을 그대로 두면서 새로운 값을 덮어쓰는 방식으로 작업하시면 됩니다. 단, 객체의 구조가 복잡해지면 (단, object.something.inside.hello.bye 처럼 객체 안의 객체 안의 객체 안의 있는 값을 바꿀때는 ... 로만 하는것은 굉장히 번거롭습니다. 리덕스의 상태는 최대한 깊지 않은 구조로 진행하는 것이 좋긴 하지만, 깊숙히 있는 값을 바꿔야 할 때 더 쉽게 바꾸는 방법에 대해서는 나중에 다뤄보게 됩니다)

// 스토어 만들기
const store = createStore(reducer);

// render 함수 만들기
const render = () => {
	const state = store.getState(); // 현재 상태를 가져옵니다. 스토어의 현재 상태를 가져올 땐 스토어의 내장함수 사용
	const { light, counter } = state; // 편의상 비구조화 할당
	if (light) {
		lightDiv.style.background = 'green';
		switchButton.innerText = '끄기';
	} else {
		lightDiv.style.background = 'gray';
		switchButton.innerText = '켜기';
	}
	counterHeadings.innerText = counter;
};

render();

//지금 리덕스의 내부 함수들을 파악하기 위해서 리액트 없이 하기 때문에 이렇게 subscribe 함수에 대한 사용법을 익혀보고 있지만, 나중엔 우리가 리액트에서 리덕스를 쉽게 사용하기 위해 react-redux 라는걸 사용하게 되는데 해당 라이브러리에서 대신 해주므로 리액트 프로젝트에서 subscribe 를 직접 해야 되는 일은 특별한 상황을 제외하고는 거의 없습니다
// 구독하기
store.subscribe(render);

// 액션을 발생시키는 것 dispatch 스토어의 내장함수 dispatch 사용

// **** 이벤트 달아주기, 액션 발생 시키기
switchButton.onclick = () => {
	store.dispatch(toggleSwitch());
};

plusButton.onclick = () => {
	store.dispatch(increment(5));
};

minusButton.onclick = () => {
	store.dispatch(decrement());
};
```
