---
title: '[React] Basic '
date: 2020-03-14 12:49:00 -0400
categories: devlog
tags: react devlog basic
---

# React 구조와 기본 원리

## Rendering

### 이터널리 오퍼레이터, &&
구분적인 

```javascript

const Loading = () => <div>Loading...</div>

class .. {
    constructor(props) {
        super(props)
        this.state = {
            loading: false
        }
    }

    comment () {
        const con = 1;
        const res =  con > 0 ? true : false
    }

    render () {
        const {loading} = this.state;
        return (
            <>
            {
                loading && <Loading/>
            }
            </Loading>
        )
    }
}
```

## LifeCycle
1. constructor
2. componentWillMount
3. render
4. componentDidMount
5. componentWillUnmount

componentDidUpdate

### constructer
### componentWillMount()
렌더링 이전

### render
### componentDidMount
렌더링 된 이후 업데이트 필요할 때

state는 render와 componentDidMount에서는 사용하면 안된다.

state는 비동기작업이기 때문에,
렌더링 과정 중에 상태의 수정을 접근하는 것은 state가 비동기작업이기 때문에 보장받지 못한다. componentDidMount는 컴포넌트 삭제되는 과정이기 떄문에 사용할 수 없다.

## Props , State

### State


## key Warning 해결

```javascript
function App() {
    const iter = [0,1,2];
    return (
        <div>
        {
            iter.map(item=> <h1 key={item}>item</h1>)
        }
        </div>
    )
}
```

key를 설정해야하는 이유
Virtual DOM

DOM Object를 제어하는 방법은 
전체 DOM Tree을 업데이트하는 퍼포먼스적인 문제점이 있기때문에
DOM을 
Virtual Dom과 새로운 Virtual Dom과 diff하여 업데이트함.

key값을 요구하는 이유는
사용자에게 언제 업데이트되는지 세팅할 수 있도록 기회를 제공함.

/* 주의사항 index로 사용하면 안된다.

비동기 처리시 중복될 위험이 있다.

레이스 컨디션에 걸리게 될 경우 예상치 못한 경우에 걸리게됨.



## State의 이해

1. setState는 render에서 호출 할 수 없다.

render함수, constructor, componentWillUnMount 함수내에서는 사용할 수 없음.

setState는 비동기적으로 실행된다.

this.setState()를 호출 한 후

this.state를 불러오면 업데이트가 반영이 안될 수 있다.

```javascript
this.setState({
    time: new Date()
    }, () => {
        console.log(this.state);
})
```

```javascript
this.setState(prevState => console.log(preState))

this.setState({test:'test'}, () => {
    console.log(this.state);
})
```


react hooks

class기반의 컴포넌트의 단점을 해결하기 위해 

재사용성에 있어서 문제가되는 경우가 많았음.

