---
title: '[React] Flux Architecture'
date: 2020-03-19 23:10:00 -0400
categories: devlog
tags: react devlog flux
---

# Flux

Facebook에서 Client-Side Web Application을 만들기 위해 사용하는 어플리케이션 아키텍쳐.

단방향 데이터 흐름을 활용해 View 컴포넌트를 구성하는 React를 보완하는 역할을 한다.

불변성을 유지하기 위해 Reducer패턴을 사용해서 기존의 데이터에 대한 수정 없이 새로운 데이터를 반환하기 위해 reducer라는 개념을 적용한다.

데이터의 단방향성이 가능한 이유
: reducer를 이용한 데이터의 불변성

Flux의 구현체 reducer

# 구조

flux의 Best Mental Model

![react-flux-1](/assets/img/post/react/react-flux-1.png)


![react-flux-2](/assets/img/post/react/react-flux-2.png)

** 동작과정

view는 사용자의 상호작용에 응답하기 위해 새로운 action을 만들어 시스템에 전파한다.

모든 데이터는 중앙 허브인 dispatcher를 통해 흐른다.

action은 dispatcher에게 action creator메소드를 제공하는데 대부분의 action은 view에서 사용자 상호작용에서 발생한다.

dispatcher는 store를 등록하기 위한 콜백을 실행한 이후에 action을 모든 store로 전달한다.

등록된 콜백을 활용해 store는 관리하고 있는 상태 중 어떤 액션이라도 관련이 있다면 전달해준다.

store는 change 이벤트를 controller-views에게 알려주고 그 결과로 데이터 계층에서의 변화가 일어난다.

controller-views는 스스로의 setState() 메소드를 호출하고 컴포넌트 트리에 속해 있는 자식 노드 모두를 다시 랜더링하게 한다

Action creator는 라이브러리에서 제공하는 도움 메소드로 메소드 파라미터에서 action을 생성하고 type 을 설정하거나 dispatcher에게 제공하는 역할

모든 action은 store가 dispatcher에 등록해둔 callback을 통해 모든 store에 전송된다.

action에 대한 응답으로 store가 스스로 갱신을 한 다음에는 자신이 변경되었다고 모두에게 알린다.

controller-view라고 불리는 특별한 view가 변경 이벤트를 듣고 새로운 데이터를 store에서 가져온 후 모든 트리에 있는 자식 view에게 새로운 데이터를 제공한다.



- Dispatcher
- Stores
- Views

### Dispatcher

Dispatcher는 Flux 어플리케이션의 중앙 허브로 모든 데이터의 흐름을 관리한다.

본질적으로 store의 콜백을 등록하는데 쓰이고, 

action을 store에 배분해주는 간단한 작동 방식

각각 store를 직접 등록하고 콜백을 제공한다. action creator가 새로운 action이 있다고 dispatcher에게 알려주면,

어플리케이션에 있는 모든 store는 해당 action을 앞서 등록한 callback으로 전달 받는다.

어플리케이션의 규모가 커지게 되면 dispatcher역할은 더욱 필수적이다. 바로 store간에 의존성을 특정적인 순서로 callback을 실행하는 과정으로 관리하기 떄문이다.

Store는 다른 store의 업데이트가 끝날 때까지 선언적으로 기다릴 수 있고 끝나는 순서에 따라 스스로 갱신된다.

### Stores

 store는 단순히 ORM 스타일의 객체 컬랙션을 관리하는 것을 넘어 어플리케이션 내의 개별적인 도메인 에서 어플리케이션의 상태를 관리한다.

 store는 자신을 dispatcher에 등록하고 callback을 제공한다. 
 
 이 callback은 action을 파라미터로 받는다. store의 등록된 callback의 내부에서는 switch문을 사용한 action 타입을 활용해서 action을 해석하고 store 내부 메소드에 적절하게 연결될 수 있는 훅을 제공한다. 
 
 여기서 결과적으로 action은 disaptcher를 통해 store의 상태를 갱신한다. store가 업데이트 된 후, 상태가 변경되었다는 이벤트를 중계하는 과정으로 view에게 새로운 상태를 보내주고 view 스스로 업데이트하게 만든다.

### Views




// 그림

- Action

- Store

- Reducers

# Get Starting
```
npm i redux --save
yarn add redux
```

##  Side Effects
상태 변화를 유도하는 모든 요소들

리덕스 스토어에 상태를 변화시키는 액션들의 모든 작업

redux-thunk -> redux-saga

es6 generater 기반 

# 참고 문서
https://haruair.github.io/flux/docs/overview.html#content

https://taegon.kim/archives/5288