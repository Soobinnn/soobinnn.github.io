---
title: '[React] React Router'
date: 2020-02-03 13:11:00 -0400
categories: devlog
tags: react devlog router
---

# React Router 란?

기본적으로 클라이언트 사이드 렌더링을 하는 SPA특징을 가지는 리액트에서 주소마다 다른 뷰를 그려주기 위해서 필요함.

- history
- location
- match

__Router Component__

- HashRouter
- BrowserRouter

1. HashRouter
    
    링크를 추적하는데 해시를 사용.
    
    정적인 서버에 적용하는 것이 적절함.

2. BrowserRouter

    동적인 서버

__history__

브라우저의 window.history와 유사
주소를 임의로 변경하거나 되돌아 갈 수 있도록 한다.
주소 변경시, SPA특성을 지키기 위해 페이지 전체를 리로드 하지 않는다.

__location__

브라우저의 window.location와 유사

현재 페이지 정보를 지니고 있다.

url의 query 정보 search라는 프로퍼티에 가지고 있다.

__match__

Route의 path에 정의한 것과 매칭된 정보를 가지고 있다.

- match.url

    실제로 매칭된 url 문자열 ex) /board/1

- match.path

    매칭에서 사용된 경로패턴 /    실제로 매칭된 url 문자열 ex) /board/1
/:id

Link

: a 태그를 기반으로 기능상의 개선을 통해 새로고침 없이 다른 뷰를 렌더 하기 위해 사용

history.push


# install

```
npm install --save react-router-dom
```

# start

## 라우터 설정

```javascript
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

```javascript
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

## 라이브러리
라우트 전환 애니메이션 작업

react-transition-group 




# 참고 문서
https://john015.netlify.com/react-router-v-5-1-%EB%AC%B4%EC%97%87%EC%9D%B4-%EB%8B%AC%EB%9D%BC%EC%A1%8C%EC%9D%84%EA%B9%8C

https://medium.com/@wdjty326/react-router-dom-v5-route-%EC%A0%84%ED%99%98-%EC%95%A0%EB%8B%88%EB%A9%94%EC%9D%B4%EC%85%98-%EC%B2%98%EB%A6%AC-935dfc6cc475