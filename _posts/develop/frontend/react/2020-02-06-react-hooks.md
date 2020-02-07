---
title: '[React] React Hooks'
date: 2020-02-06 17:31:00 -0400
categories: devlog
tags: react devlog hooks
---

# React Hooks 란?

Hook를 이용하여 Class를 작성하지 않고 함수형에서 상태관리, React Component LifeCycle을 설정할 수 있게 하여 기존 함수형 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 해줌.

React v 16.8에 새로 도입된 기능

## Hook 종류

- useState
- useEffect
- useContext
- useReducer
- useMemo
- useCallback
- useRef
- useInputs
- usePromise

## useState

### example

```javascript
import React, { useState } from 'react';

// ES6버전에서 사용하는 화살표 함수를 사용했습니다.
const Example = () => {
	// 새로운 state 변수를 선언하고, count라 부르겠습니다.
	const [count, setCount] = useState(0);

	return (
		<div>
			<p>You clicked {count} times</p>
			<button onClick={() => setCount(count + 1)}>Click me</button>
		</div>
	);
};
```

# Hooks LifeCycle

## useEffect

Hooks로 라이프사이클을 다루기 위해서는 useEffect가 필요함.

useEffect 는 기본적으로 렌더링 되고난 직후마다 실행되며, 두번째 파라미터 배열에 무엇을 넣느냐에 따라 실행되는 조건이 달라진다.

### componentDidMount

#### Example

```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // useEffect는 첫번째 인자로 callBack함수를 받습니다.
  useEffect(() => {
    // 컴포넌트가 마운트 되고 setTimeout함수를실행합니다.
    setTimeout(() => {
        document.title = `You clicked ${count} times`;
    }, 3000);
  }, []); <--- 두번째 인자로 빈 배열 넣어주기

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

useEffect함수를 Mount되고 한번만 실행하게 하려면 두번째 인자로 빈 배열을 넣어줘야한다.

그렇지 않을 경우, state값이 update 될 경우 다시 한번 렌더링을 해줌.

### componentDidUpdate

#### Example

```javascript
import React, { useState, useEffect } from 'react';

function Example() {
	const [count, setCount] = useState(0);

	// useEffect는 첫번째 인자로 callBack함수를 받습니다.
	useEffect(() => {
		// 컴포넌트가 업데이트 되고 setTimeout함수를 실행합니다.
		setTimeout(() => {
			document.title = `You clicked ${count} times`;
		}, 3000);
	}, [count]); //<------

	return (
		<div>
			<p>You clicked {count} times</p>
			<button onClick={() => setCount(count + 1)}>Click me</button>
		</div>
	);
}
```

useEffect는 count state를 지켜보다가 count가 갱신되면 첫번째 인자로 넣어주었던 함수를 실행하게 된다.

### componentWillUnmount

만약 컴포넌트가 언마운트되기 전이나, 업데이트 되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect 에서 뒷정리(cleanup) 함수를 반환해주어야 한다.

#### Example

```javascript
import React, { useEffect, useState } from 'react';
import ReactDOM from 'react-dom';

// Scroll을 움직이면 h1의 스타일을 변화해주기 위한 함수.
const useScroll = () => {
	// state를 생성합니다.
	const [state, setState] = useState({
		x: 0,
		y: 0
	});
	// scrll의 값을 가져와 state를 갱신합니다.
	const onScroll = () => {
		setState({ y: window.scrollY, x: window.scrollX });
	};
	useEffect(() => {
		// scroll 이벤트를 만들어줍니다. 스크롤을 움직일때 마다
		// onScroll 함수가 실행됩니다.
		window.addEventListener('scroll', onScroll);
		return () => window.removeEventListener('scroll', onScroll); // <----
	}, []);
	return state;
};

const App = () => {
	const { y } = useScroll();
	return (
		<div style={{ height: '1000vh' }} className='App'>
			<h1 style={{ position: ' fixed', color: y > 100 ? 'red' : 'blue' }}>Hi</h1>
		</div>
	);
};

const rootElement = document.getElementById('root');
ReactDOM.render(<App />, rootElement);
```

## useContext

Hook를 사용하면 함수형 컴포넌트에서 Context를 보다 더 쉽게 사용할 수 있다.

## useReducer

useState보다 컴포넌트에서 더 다양한 상황에 따라 다양한 상태를 다른 값으로 업데이트해주고 싶을 때 사용하는 Hook

Reducer는 현재 상태와, 업데이트를 위해 필요한 정보를 담은 액션 값을 전달 받아 새로운 상태를 반환하는 함수이다. 리듀서 함수에서 새로운 상태를 만들 때는 꼭 불변성을 지켜줘야한다.

```javascript
function reducer(state, action) {
  return { ... }; // 불변성을 지키면서 업데이트한 새로운 상태를 반환
}
```

Redux에서 액션 객체에는 어떤 액션인지 알려주는 type 필드가 꼭 있어야 하지만,

useReducer에서 사용하는 액션 객체는 꼭 type을 지니고 있을 필요가 없다. 심지어, 객체가 아니라 문자열이나, 숫자여도 상관없다.

### Example

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
	// action.type 에 따라 다른 작업 수행
	switch (action.type) {
		case 'INCREMENT':
			return { value: state.value + 1 };
		case 'DECREMENT':
			return { value: state.value - 1 };
		default:
			// 아무것도 해당되지 않을 때 기존 상태 반환
			return state;
	}
}

const CounterUseReducer = () => {
	const [state, dispatch] = useReducer(reducer, { value: 0 });

	return (
		<div>
			<p>
				현재 카운터 값은 <b>{state.value}</b> 입니다.
			</p>
			<button onClick={() => dispatch({ type: 'INCREMENT' })}>+1</button>
			<button onClick={() => dispatch({ type: 'DECREMENT' })}>-1</button>
		</div>
	);
};

export default CounterUseReducer;
```

useReducer 의 첫번째 파라미터는 리듀서 함수,두번째 파라미터는 해당 리듀서의 기본 값을 넣어준다.

이 Hook 을 사용 했을 때에는 state 값과 dispatch 함수를 받아오게 되는데 여기서 state 는 현재 가르키고 있는 상태고, dispatch 는 액션을 발생시키는 함수이다.

dispatch(action)와 같은 형태로, 함수 안에 파라미터로 액션 값을 넣어주면 리듀서 함수가 호출되는 구조

useReducer를 사용했을 때의 장점은 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 점

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
	return {
		...state,
		[action.name]: action.value
	};
}

const Info = () => {
	const [state, dispatch] = useReducer(reducer, {
		name: '',
		nickname: ''
	});
	const { name, nickname } = state;
	const onChange = e => {
		dispatch(e.target);
	};

	return (
		<div>
			<div>
				<input name='name' value={name} onChange={onChange} />
				<input name='nickname' value={nickname} onChange={onChange} />
			</div>
			<div>
				<div>
					<b>이름:</b> {name}
				</div>
				<div>
					<b>닉네임: </b>
					{nickname}
				</div>
			</div>
		</div>
	);
};

export default Info;
```

useReducer에서의 액션은 그 어떤 값이 되어도 된다. 그래서 이벤트 객체가 지니고있는 e.target 값 자체를 액션 값으로 사용함.

이런 식으로 인풋을 관리하면, 아무리 인풋의 개수가 많아져도 코드를 짧고 깔끔하기 유지 할 수 있다.

## useMemo

함수형 컴포넌틍 내부에서 발생하는 연산을 최적화 할 수 있다.

## useCallback

useMemo와 상당히 비슷한 함수. 렌더링 성능을 최적화해야하는 상황에서 사용함.

이 Hook을 사용하면 이벤트 핸들러 함수를 필요할 때만 생성 할 수 있습니다.

Average라는 함수컴포넌트 안에 onChange 와 onInsert 라는 함수를 선언했다고 가정한다면, 이렇게 선언을 하게 되면 컴포넌트가 리렌더링 될 때마다 이 함수들이 새로 생성됨.

대부분의 경우에는 이러한 방식이 문제가 되지 않지만, 컴포넌트의 렌더링이 자주 발생하거나, 렌더링 해야 할 컴포넌트의 개수가 많아진다면 이 부분을 최적화 해주시는 것이 좋다.

아래 코드는 똑같은 코드이다.

```javascript
useCallback(() => {
	console.log('hello world!');
}, []);

useMemo(() => {
	const fn = () => {
		console.log('hello world!');
	};
	return fn;
}, []);
```

useCallback은 결국 useMemo 에서 함수를 반환하는 상황에서 더 편하게 사용 할 수 있는 Hook 이다.

숫자, 문자열, 객체 처럼 일반 값을 재사용하기 위해서는 useMemo 를, 그리고 함수를 재사용 하기 위해서는 useCallback 을 사용

## useRef

함수형 컴포넌트에서 ref 를 쉽게 사용 할 수 있게 해준다

useRef 를 사용하여 ref 를 설정하면, useRef 를 통해 만든 객체 안의 current 값이 실제 엘리먼트를 가르키게 됩니다

컴포넌트 로컬 변수를 사용해야 할 때도 useRef 를 활용 할 수 있다.

여기서 로컬 변수라 함은, 렌더링이랑은 관계 없이 바뀔 수 있는 값을 의미

```javascript
import React, { Component } from 'react';

class MyComponent extends Component {
	id = 1;
	setId = n => {
		this.id = n;
	};
	printId = () => {
		console.log(this.id);
	};
	render() {
		return <div>MyComponent</div>;
	}
}

export default MyComponent;
```

```javascript
import React, { useRef } from 'react';

const RefSample = () => {
	const id = useRef(1);
	const setId = n => {
		id.current = n;
	};
	const printId = () => {
		console.log(id.current);
	};
	return <div>refsample</div>;
};

export default RefSample;
```

주의 하실 점은, 이렇게 넣는 ref 안의 값은 바뀌어도 컴포넌트가 렌더링 되지 않는다는 점 입니다. 렌더링과 관련 되지 않은 값을 관리 할 때만 이러한 방식으로 코드를 작성 .

## usePromise

함수형 컴포넌트에서 Promise를 더 쉽게 사용할 수 있는 Hook

useEffect 를 사용하실 때 주의 할 점이 있는데, useEffect 에 파라미터로 전달해주는 함수에서 async 를 사용하면 안된다. 예를 들어서 다음 코드는 오류를 발생하는 코드이다.

```javascript
useEffect(async () => {});
```

### Custom Hooks

[https://nikgraf.github.io/react-hooks/](https://nikgraf.github.io/react-hooks/)

[https://github.com/rehooks/awesome-react-hooks](https://github.com/rehooks/awesome-react-hooks)

# 참고 문서

https://velog.io/@velopert/react-hooks
