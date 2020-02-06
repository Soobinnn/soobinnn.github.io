---
title: '[React] Dev Tool'
date: 2020-02-06 14:39:00 -0400
categories: devlog
tags: react devlog dev tool
---

# React 개발자 도구

- mobx DevTool
- Redux DevTool

## mobx DevTool

mobx-react@6이상은 더 이상 mobx-react-devtools와 호환되지 않습니다. 즉, MobX react devtools는 더 이상 컴포넌트의 렌더링 타이밍 또는 종속성 트리를 표시하지 않습니다. 그 이유는 표준 React devtools가 다시 렌더링 컴포넌트를 강조 할 수 있기 때문입니다. 그리고 아래 이미지와 같이 표준 devtools로 구성 요소의 종속성 트리를 검사할 수 있다.

### React Devtools 플러그인

### mobx-logger

[https://github.com/winterbe/mobx-logger](https://github.com/winterbe/mobx-logger)

```
npm install mobx-logger
```

## Redux DevTool

리덕스 개발을 편리하게 하기 위해 Redux DevTools라는 크롬 확장프로그램을 활용하면 편함.

### Install

[https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)

### Setting

설치 후, 리액트 프로젝트에 src/index.js에 코드 추가

```javascript
# src/index.js
....
import App from './App';
import { createStore } from 'redux';
import rootReducer from './store/modules';

// **** 리덕스 개발자도구 적용
const devTools =
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__();

const store = createStore(rootReducer, devTools);

ReactDOM.render(<App />, document.getElementById('root'));
....
```

### 실행화면

해당 리액트 프로젝트를 실행시키고 크롬에서 F12를 누르면 Redux메뉴가 생긴 것을 확인할 수 있다. ![react-redux-devtool-1](/assets/img/post/react/react-redux-devtool-1.PNG)
