---
title: '[React] React Router'
date: 2020-02-03 13:11:00 -0400
categories: devlog
tags: react devlog router
---

# React Router 란?

# install

```
npm install --save react-router-dom
```

# start

## 라우터 설정

```
# src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Router, Route, IndexRoute, browserHistory } from 'react-router';

import App from './App';
import Home from './containers/Home';
import About from './containers/About';
import Posts from './containers/Posts';

import './index.css';

ReactDOM.render(
   <Router>
        <Route exact path="/" component={App}/>
        <Route path="/home" component={Home}/>
        <Route path="/about" component={About}/>
        <Route path="/post" component={Posts}/>
    </Router>,
  document.getElementById('root')
);
```

react-router에서 4가지의 객체 불러옴.

Router react-router의 주요 컴포넌트로, 라우터의 속성 정의 및 내부에서 라우트 설정

Route 설정한 경로에서 어떤 컴포넌트를 렌더링 할 지 정하는 컴포넌트

라우트 컴포넌트 자식에 또 다른 Route컴포넌트를 넣으면

해당 자식 컴포넌트는 부모 라우트의 서브 라우트가 됨.

- exact 옵션 : 주어진 경로와 정확히 맞아 떨어져야만 설정한 컴포넌트를 보여줍니다.

IndexRoute 서브라우트가 주어지지 않았을 때, (특정 라우트의 / 경로로 들어 왔을 때)

이 라우트에서 지정한 컴포넌트를 보여줌

browserHistory History API를 사용하여 브라우저의 url 변화를 주시하고 조작함.

<Router history={browserHistory}/>

history는 브라우저의 주소창이 어떻게 바뀌는지 주시하고 주소를 라우터에서 인식할 수 있도록 location 객체로 파싱해줌.

(history는 총 3가지)

<Route path="/" component={App}>

/ 경로로 들어왔을 때 App 컴포넌트를 보여주라고 설정

자식 Route들은 url이 매칭하는 경우 App컴포넌트의 자식으로 들어감.

ex) /about - ABOUT경로

```
# src/components/Header.js
import React from 'react';
import { Link } from 'react-router';
import './Header.css';


const MenuItem = ({active, children, to}) => (
    <Link to={to} className="menu-item">
            {children}
    </Link>
)


const Header = () => {
    return (
        <div>
            <div className="logo">
                microblog
            </div>

            <div className="menu">
                <MenuItem to={'/'}>홈</MenuItem>
                <MenuItem to={'/about'}>소개</MenuItem>
                <MenuItem to={'/post'}>포스트</MenuItem>
            </div>
        </div>
    );
};

export default Header;

```

Link컴포넌트에 className을 설정하면 그대로 전달돼서 해당 클래스를 가진 a태그로 이뤄진 컴포넌트로 변환해줌.

Link컴포넌트가 눌렀을 때, 설정 될 라우트 경로는 to값을 통해 설정함.
