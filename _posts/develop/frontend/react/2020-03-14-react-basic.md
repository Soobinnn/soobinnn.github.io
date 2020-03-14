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
