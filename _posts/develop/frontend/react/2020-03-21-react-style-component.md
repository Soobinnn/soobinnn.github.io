---
title: '[React] Style Component'
date: 2020-03-19 23:10:00 -0400
categories: devlog
tags: react devlog style css
---

```
```
# Style Component
[https://styled-components.com/](https://styled-components.com/)

# 
정적 데이터

리버스 프록시, nginx

# Get Starting

## Install
```
npm i styled-components --save
```

## Use
```javascript
import styled from 'styled-components'

const Componet = styled.h1`
    display: block;
`
const App = () => {
    return (
        <Component/>
    );
}
```

## Add Plugin
styled-component snippet, Extractor


# 특징
조건 렌더링

css가 특정한 값이 true일 경우에 조건에 따라 렌더링을 할 수 있다.

기존의 css는 javascript는 분리 되어 있음.

inline의 경우는 코드의 가독성, 유지보수 측면에서 권장하지 않음.

css요소를 자바스크립트 component안에 동적으로 사용할 수 있도록 만듦으로써 스타일링을 코드를 자바스크립트로 동일하게 통일 할 수 있다.

/* html코드가 javascript안에 넣은것이 jsx

상속을 받아 객체지향적으로 사용할 수 있다.


# Example
```javascript
import styled from 'styled-components'

const color = 'black'

const Componet = styled.div`
    display: ${props => props.isLoaded ? 'block' :'none'};
    color: ${color};
`

const Wrapper = styled(Component)`
    background-color: gray;
    margin: 20px;
`

const App = () => {
    return (
        <Wrapper isLoaded>
            <Component isLoaded/>
        </Wrapper>
    );
}
```

