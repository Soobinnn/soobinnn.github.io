---
title: '[React] Mobx'
date: 2020-02-05 11:59:00 -0400
categories: devlog
tags: react devlog mobx store
header-img: '/img/logo/mobx-logo.png'
---

# Mobx 란?

리액트 상태 관리 라이브러리.

최소한의 공수로 상태관리 시스템을 설계해줌.

## Mobx 장점

1. 객체지향적

2. 서버개발자에게 친숙한 아키텍쳐

3. Decorator

4. 캡슐화

5. 불변성 유지를 위한 노력 불필요


# Mobx 개념

- Observable State ( 관찰 받고 있는 상태)
- Computed Value (연산된 값)
- Reactions (반응)
- Actions (행동)

## Observable State

상태를 관찰할 수 있는 상태. 앱에서 특정 부분이 바뀌, Mobx에서 어떤 부분이 바뀌었는지 알 수 있다.

## Computed Value

기존의 상태 값과 다른 연산된 값에 기반하여 만들질 수 있는 값.

성능 최적화를 위하여 많이 사용됨.

어떤 값을 연산해야 할 때, 연산에 기반되는 값이 바뀔때만 새로 연산하게 하고, 바뀌지 않았다면 그냥 기존의 값을 사용할 수 있게 해줌.

## Reactions

Computed Value와 비슷함.

Computed Value의 경우 특정 값을 연산해야 될 때에만 처리가 되는 반면에, <br/> Reactions은 값이 바뀜에 따라 해야 할 일을 정하는 것을 의미.

## Actions

상태에 변화를 일으키는 것을 말함. 만약 Observable State에 변화를 일으키는 코드를 호출하면 하나의 액션이된다.

리덕스에서의 액션과 달리 따로 객체형태로 만들지 않는다.

## autorun

reaction, computed의 observe대신에 사용 될 수 있다.

autorun으로 전달해주는 함수에서 사용되는 값이 있으면 자동으로 그 값을 주시하여 그 값이 바뀔 때마다 함수가 주시되도록 해준다. 여기서 만약 computed로 만든 값의 .get()함수를 호출해주면, 하나하나 observe해주지 않아도 된다.

## transaction

액션을 한꺼번에 일으키는 것

### example1

```javascript
import { observable, reaction, computed, autorun } from 'mobx';

// Observable State 만들기
const calculator = observable({
	a: 1,
	b: 2
});

// **** 특정 값이 바뀔 때 특정 작업 하기!
reaction(
	() => calculator.a,
	(value, reaction) => {
		console.log(`a 값이 ${value} 로 바뀌었네요!`);
	}
);

reaction(
	() => calculator.b,
	value => {
		console.log(`b 값이 ${value} 로 바뀌었네요!`);
	}
);

// **** computed 로 특정 값 캐싱
const sum = computed(() => {
	console.log('계산중이예요!');
	return calculator.a + calculator.b;
});

sum.observe(() => calculator.a); // a 값을 주시
sum.observe(() => calculator.b); // b 값을 주시

calculator.a = 10;
calculator.b = 20;

//**** 여러번 조회해도 computed 안의 함수를 다시 호출하지 않지만..
console.log(sum.value);
console.log(sum.value);

// 내부의 값이 바뀌면 다시 호출 함
calculator.a = 20;
console.log(sum.value);
```

### example 2

reaction, computed의 observe대신 autorun 사용한 코드

```javascript
import { observable, reaction, computed, autorun } from 'mobx';

// Observable State 만들기
const calculator = observable({
	a: 1,
	b: 2
});

// computed 로 특정 값 캐싱
const sum = computed(() => {
	console.log('계산중이예요!');
	return calculator.a + calculator.b;
});

// **** autorun 은 함수 내에서 조회하는 값을 자동으로 주시함
autorun(() => console.log(`a 값이 ${calculator.a} 로 바뀌었네요!`));
autorun(() => console.log(`b 값이 ${calculator.b} 로 바뀌었네요!`));
autorun(() => sum.get()); // su

calculator.a = 10;
calculator.b = 20;

// 여러번 조회해도 computed 안의 함수를 다시 호출하지 않지만..
console.log(sum.value);
console.log(sum.value);

calculator.a = 20;

// 내부의 값이 바뀌면 다시 호출 함
console.log(sum.value);
```

### example3

# Install & Setting

1. CRA로 프로젝트가 생성되었다고 가정한다.

```
create-react-app <project_name>
```

2. Add react-app-rewired and customize-cra, and any Babel plugins you want to use

```
yarn add --dev customize-cra react-app-rewired @babel/plugin-proposal-decorators

```

3.  package.json scripts 변경

```
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test",
  "eject": "react-scripts eject"
}
```

4. 프로젝트 root 에 config-overrides.js 생성

```
const { override, addDecoratorsLegacy } = require('customize-cra')

// Adds legacy decorator support to the Webpack configuration.
module.exports = override(addDecoratorsLegacy())
```

5. mobx 라이브러리 설치

```
yarn add mobx mobx mobx-react
```

6. Provider로 프로젝트에 스토어 적용예제를 따로 만들지 않았으므로 주석으로 설정방법만 작성해 놓았다.

```javascript
# src/index.js

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { Provider } from 'mobx-react';
//import CounterStore from './stores/counter'; //스토어 불러와줍니다.

//const counter = new CounterStore(); // 스토어 인스턴스 생성

// <Provider counter={counter}> 스토어를 Provider로 넣어줌
ReactDOM.render(
	<Provider>
		<App />
	</Provider>,
	document.getElementById('root')
);

serviceWorker.unregister();

```

## mobx-react-devtools 개발도구

mobx-react-devtools는 어떤 값을 바꿨을 때 어떠한 컴포넌트들이 영향을 받고, 업데이트는 얼마나 걸리고, 어떠한 변화가 일어났는지에 대한 세부적인 정보를 볼 수 있게 해준다.

```
yarn add mobx-react-devtools
```

```javascript
# src/App.js

import React from 'react';
import './App.css';
import DevTools from 'mobx-react-devtools';

function App() {
	return (
		<div>
      ...
			{process.env.NODE_ENV === 'development' && <DevTools />}
		</div>
	);
}

export default App;

```

## 스토어 끼리 관계형성

스토어와 스토어 간에 접근을 해야할 때,

1.  RootStore 생성

```javascript
# src/stores/index.js

import 스토어1 from './~~';
import 스토어2 from './~~';

class RootStore {
  constructor() {
    this.스토어1 = new 새로운스토어(this);
    this.스토어2 = new 새로운스토어(this);
  }
}

export default RootStore;

```

2. 각 스토어에 constructor를 생성한다.

```javascript
# src/stores/스토어1.js
class default class 스토어1 {

constructor(root) {
  this.root = root;
}

...

}
```

3. index.js - Provider설정

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { Provider } from 'mobx-react';
import RootStore from './Stores';

const root = new RootStore(); // *** 루트 스토어 생성

ReactDOM.render(
	<Provider {...root}>
		<App />
	</Provider>,
	document.getElementById('root')
);

serviceWorker.unregister();
```

\* 만약 store1에서 store2에 접근하고싶다면, store1에서 this.root.store2으로 접근하면됨.

## Mobx

리스트를 렌더링 할 때에 내부에 있는 컴포넌트에도 observer 를 구현해주어야, 성능적으로 최적화가 일어난다

## Mobx 리액트 컴포넌트 최적화

성능이 망가지지 않으려면, 지켜야할 규칙이있다.

1. 리스트를 렌더링 할 땐, 컴포넌트에 리스트 관련 데이터만 props로 넣자
2. 세부참조(dereference)는 최대한 늦게하자
3. 함수는 미리 바인딩하고, 파라미터는 내부에서 넣어주기

### 1. 리스트를 렌더링 할 땐, 컴포넌트에 리스트 관련 데이터만 props로 넣자

리스트가 렌더링 될 때는 성능에 대해서 신경을 써줘야하는데, 리스트 컴포넌트에 리스트 관련된 props만 넣는것을 권장함.

```javascript

# Bad Code
@observer class MyComponent extends Component {
   render() {
       const {todos, user} = this.props;
       return (<div>
           {user.name}
           <ul>
               {todos.map(todo => <TodoView todo={todo} key={todo.id} />)}
           </ul>
       </div>)
   }
}
```

위와 같은 코드에서 user.name이 바뀔 때도 컴포넌트가 리렌더링 되기 때문에 별로 좋지 않다.

아예 리스트를 잘 분리시켜서 리스트는 리스트가 바뀔시에만 렌더링이 되도록 하는것이 좋다.

```javascript
# Good Code

@observer class MyComponent extends Component {
   render() {
       const {todos, user} = this.props;
       return (<div>
           {user.name}
           <TodosView todos={todos} />
       </div>)
   }
}

@observer class TodosView extends Component {
   render() {
       const {todos} = this.props;
       return <ul>
           {todos.map(todo => <TodoView todo={todo} key={todo.id} />)}
       </ul>)
   }
}
```

### 2. 세부참조(dereference)는 최대한 늦게하자

새부 참조 (혹은 역참조) 란, 우리가 특정 객체의 내부의 값을 조회하는것

```javascript
# Bad Code
 const itemList = items.map(item => (
    <BasketItem
      name={item.name}
      price={item.price}
      count={item.count}
      key={item.name}
      onTake={onTake}
    />
  ));

```

```javascript
# Good Code

 const itemList = items.map(item => (
    <BasketItem
      item={item}
      key={item.name}
      onTake={onTake}
    />
  ));
```

변동이 일어날 수 있는 count값의 세부참조를 자식 컴포넌트 내부에서 하게 된다면, 더 높은 성능으로 컴포넌트를 업데이트 할 수 있다.

(\* 위 코드에서 item.name 값은 바뀌지 않기 떄문에 key로 설정한 것)

### 3. 함수는 미리 바인딩하고, 파라미터는 내부에서 넣어주기

컴포넌트에 함수를 전달해 줄 때에는 미리 바인딩 하는 것이 좋고,

파라미터가 유동적일 땐 파라미터를 넣는 작업을 컴포넌트 밖이 아니라 안에서 하는 것이 좋다.

```javascript
# Bad Code

render() {
    return <MyWidget onClick={() => { alert('hi') }} />
}
```

```javascript
render() {
    return <MyWidget onClick={this.handleClick} />
}

handleClick = () => {
    alert('hi')
}
```

```javascript
# Bad Code

const ShopItemList = ({ onPut }) => {
  const itemList = items.map(item => (
    <ShopItem {...item} key={item.name} onPut={() => onPut(item.name, item.price)} />
  ));
  return <div>{itemList}</div>;
};
```

```javascript
# Good Code

const ShopItemList = ({ onPut }) => {
  const itemList = items.map(item => (
    <ShopItem {...item} key={item.name} onPut={onPut} />
  ));
  return <div>{itemList}</div>;
};

const ShopItem = ({ name, price, onPut }) => {
  return (
    <div className="ShopItem" onClick={() => onPut(name, price)}>
      <h4>{name}</h4>
      <div>{price}원</div>
    </div>
  );
};
```

# 참고 문서

https://velog.io/@velopert/MobX-3-%EC%8B%AC%ED%99%94%EC%A0%81%EC%9D%B8-%EC%82%AC%EC%9A%A9-%EB%B0%8F-%EC%B5%9C%EC%A0%81%ED%99%94-%EB%B0%A9%EB%B2%95-tnjltay61n#3-2.-mobx-%EC%9D%98-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%B5%9C%EC%A0%81%ED%99%94

https://woowabros.github.io/experience/2019/01/02/kimcj-react-mobx.html