---
title: '[StoryBook] StoryBook'
date: 2020-01-21 23:21:00 -0400
categories: devlog
tags: tool devlog storybook react
---

# StoryBook 이란?

UI 컴포넌트를 직접 보면서 개발을 할 수 있는 환경을 제공하는 툴

토리북은 프로젝트 내에서 독립된 환경으로 실행 되기 때문에, 앱의 특정한 의존성에서 벗어나서 순수 UI 개발에 집중 할 수 있도록 한다

또한, 스토리북은 리액트 웹(Web) 뿐만 아니라 리액트 네이티브(React Native) 환경에서도 사용 할 수 있다.

스토리북을 활용하면 개발자 본인 뿐 아니라, 팀(기획자, 디자이너)과의 협업 구조에서도 원할한 커뮤니케이션과 빠른 이터레이션(iteration)을 통한 개발 생산성 향상 효과도 누릴 수 있다.

UI 개발을 하다 보면 빈번하게 일어나는 디자인 스펙 오류, 기획 프로세스 오류 등을 빠르게 확인 하여 수정 할 수 있으며, 개발자는 컴포넌트를 더욱 유연하고, 재사용 가능한 컴포넌트 개발을 할 수 있도록 도와준다.

# install

## React에서 사용하기

```
npm install -g @storybook/cli

getstorybook init

npm run storybook 또는
yarn storybook
```

### 애드온 설치

#### Knobs

컴포넌트의 props를 스토리북 화면에서 바꿔서 바로 반영시켜줄 수 있는 애드온

```
yarn add --dev @storybook/addon-knobs
```

#### Actions

컴포넌트를 통하여 특정 함수가 호출됐을 때 어떤 함수가 호출됐는지, 그리고 함수에 어떤 파라미터를 넣어서 호출했는지에 대한 정보를 확인 할 수 있게 해줌.

간단한 함수 호출부터 시작해서, 나중에는 리액트 라우터의 주소가 변경될 때를 확인하거나, 리덕스 스토어의 dispatch를 mocking하여 디스패치 되는 액션의 정보를 볼 수 도 있음.

Storybook CLI로 만든 프로젝트에 **기본적으로 적용이 되어있기 때문에 별도로 설치하실 필요가 없다.**

#### Docs

MDX형식으로 문서를 작성 할 수 있게 해주고, 컴포넌트의 props와 주석에 기반하여 문서를 자동생성해줌.

```
yarn add --dev @strorybook/addon-docs
```

# 참고자료

https://velog.io/@velopert/start-storybook
