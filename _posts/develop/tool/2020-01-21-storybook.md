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

stories 디렉토리와 .storybook 디렉토리가 생성된 것을 확인 할 수 있다.

# Start

## Setting

경로 ../src/\*_/_.stories.js확인

```javascript
# .storybook/config.js
module.exports = {
  stories: ['../src/**/*.stories.js'],
  addons: [
    '@storybook/preset-create-react-app',
    '@storybook/addon-actions',
    '@storybook/addon-links',
  ],
};
```

## Example

예제 코드

```javascript
# src/Components/Hello.js
import React from 'react';

const Hello = ({ name, big }) => {
  if (big) {
    return <h1>안녕하세요 {name}!</h1>;
  }
  return <p>안녕하세요, {name}!</p>;
};

export default Hello;
```

스토리 작성

스토리를 작성할 때에는 .stories.js 확장자로 작성하면됨.

Storybook v5.2 부터는 Component Story Format (CSF) 형식을 사용하여 문서를 작성함.

```javascript
# src/stories/Hello.stories.js
import React from 'react';
import Hello from '../Components/Hello';

export default {
  title: 'components|basic/Hello', // 스토리북에서 보여질 그룹과 경로를 명시
  component: Hello, // 어떤 컴포넌트를 문서화 할지 명시
};

export const standard = () => <Hello name="Storybook" />;
export const big = () => <Hello name="Storybook" big />;
```

**yarn storybook**

**실행화면**

![storyboard-1](/assets/img/post/react/react-storyboard-1.PNG)

StoryBook의 가장 기본적인 기능이다.

## 애드온

StoryBook Addon을 적용하면 더욱 다양하고 편리한 기능들을 붙여줄 수 있다.

- Knobs
- Action
- Docs
- Viewport

### Knobs

컴포넌트의 props를 스토리북 화면에서 바꿔서 바로 반영시켜줄 수 있는 애드온

#### Install

```
yarn add --dev @storybook/addon-knobs
```

#### Setting

**.storybook/main.js 에 @storybook/addon-knobs/register 추가**

```
module.exports = {
  stories: ['../src/**/*.stories.js'],
  addons: ['@storybook/preset-create-react-app', '@storybook/addon-actions', '@storybook/addon-links', '@storybook/addon-knobs/register'],
};
```

```javascript
# src/stories/Hello.stories.js
import React from 'react';
import Hello from '../Components/Hello';
import { withKnobs } from '@storybook/addon-knobs';

export default {
  title: 'components|basic/Hello', // 스토리북에서 보여질 그룹과 경로를 명시
  component: Hello, // 어떤 컴포넌트를 문서화 할지 명시
  decorators: [withKnobs] // 애드온 적용
};

export const standard = () => <Hello name="Storybook" />;
export const big = () => <Hello name="Storybook" big />;
```

#### Example - Knobs 생성

Knobs 를 사용 할 때 넣어주어야 하는 주요 인자로는 Knobs 의 이름, 기본값 그리고 GROUP ID 가 있다. (GROUP ID 의 경우 생략가능)

```javascript
# src/stories/Hello.stories.js
import React from 'react';
import Hello from '../Components/Hello';
import { withKnobs, text, boolean } from '@storybook/addon-knobs';

export default {
	title: 'components|basic/Hello', // 스토리북에서 보여질 그룹과 경로를 명시
	component: Hello, // 어떤 컴포넌트를 문서화 할지 명시
	decorators: [withKnobs] // 애드온 적용
};

export const hello = () => {
	// knobs 만들기
	const big = boolean('big', false, 'Group 1');
	const name = text('name', 'Storybook');
	return <Hello name={name} big={big} />;
};
hello.story = {
	name: 'Default'
};

export const standard = () => <Hello name='Storybook' />;
export const big = () => <Hello name='Storybook' big />;
```

**실행 화면**

![storyboard-2](/assets/img/post/react/react-storyboard-2.PNG)

#### Knobs 종류

- text: 텍스트를 입력 할 수 있습니다.
- boolean: true/false 값을 체크박스로 설정 할 수 있습니다.
- number: 숫자를 입력 할 수 있습니다. 1~10과 같이 간격을 설정 할 수도 있습니다.
- color: 컬러 팔레트를 통해 색상을 설정 할 수 있습니다.
- object: JSON 형태로 객체 또는 배열을 설정 할 수 있습니다.
- array: 쉼표로 구분된 텍스트 형태로 배열을 설정 할 수 있습니다.
- select: 셀렉트 박스를 통하여 여러가지 옵션 중에 하나를 선택 할 수 있습니다.
- radios: Radio 버튼을 통하여 여러가지 옵션 중에 하나를 선택 할 수 있습니다.
- options: 여러가지 옵션을 선택 하는 UI 를 커스터마이징 할 수 있습니다 (radio, inline-radio, check, inline-check, select, multi-select)
- files: 파일을 선택 할 수 있습니다.
- date: 날짜를 선택 할 수 있습니다.
- button: 특정 함수를 실행하게 하는 버튼을 만들 수 있습니다.

### Actions

컴포넌트를 통하여 특정 함수가 호출됐을 때 어떤 함수가 호출됐는지, 그리고 함수에 어떤 파라미터를 넣어서 호출했는지에 대한 정보를 확인 할 수 있게 해줌.

간단한 함수 호출부터 시작해서, 나중에는 리액트 라우터의 주소가 변경될 때를 확인하거나, 리덕스 스토어의 dispatch를 mocking하여 디스패치 되는 액션의 정보를 볼 수 도 있음.

Storybook CLI로 만든 프로젝트에 **기본적으로 적용이 되어있기 때문에 별도로 설치하실 필요가 없다.**

#### Example

```javascript
# src/Components/Hello.js

import React from 'react';

const Hello = ({ name, big, onHello, onBye }) => {
  return (
    <div>
      {big ? <h1>안녕하세요 {name}!</h1> : <p>안녕하세요 {name}!</p>}
      <div>
        <button onClick={onHello}>Hello</button>
        <button onClick={onBye}>Bye</button>
      </div>
    </div>
  );
};

export default Hello;

```

```javascript
# src/stories/Hello.stories.js

import React from 'react';
import Hello from '../Components/Hello';
import { withKnobs, text, boolean } from '@storybook/addon-knobs';
import { action } from '@storybook/addon-actions';

export default {
  title: 'components|basic/Hello', // 스토리북에서 보여질 그룹과 경로를 명시
  component: Hello, // 어떤 컴포넌트를 문서화 할지 명시
  decorators: [withKnobs], // 애드온 적용
};

export const hello = () => {
  // knobs 만들기
  const big = boolean('big', false, 'Group 1');
  const name = text('name', 'Storybook');
  return <Hello name={name} big={big} onHello={action('onHello')} onBye={action('onBye')} />;
};
hello.story = {
  name: 'Default',
};

export const standard = () => <Hello name="Storybook" />;
export const big = () => <Hello name="Storybook" big />;
```

**실행 화면**

![storyboard-3](/assets/img/post/react/react-storyboard-3.PNG)

### Docs

MDX형식으로 문서를 작성 할 수 있게 해주고, 컴포넌트의 props와 주석에 기반하여 문서를 자동생성해줌.

#### Install

```
yarn add --dev @storybook/addon-docs
```

#### Setting

**1) .storybook/main.js에 @storybook/addon-docs/react/preset 추가** **2) .mdx 확장자도 처리하도록 정규식을 수정**

```
module.exports = {
  stories: ['../src/**/*.stories.(js|mdx)'],
  addons: ['@storybook/preset-create-react-app', '@storybook/addon-actions', '@storybook/addon-links', '@storybook/addon-knobs/register'],
};
```

**StoryBook 서버 종료 후 재시작**

상단에 Docs 가 생성된 것을 확인 할 수 있다.

![storyboard-4](/assets/img/post/react/react-storyboard-4.PNG)

#### Start

지금은 Props 부분이 "No props found for this component" 라고 보여지면서 비어있다.

이 부분을 채우려면 prop-types 또는 TypeScript를 사용해야합

**문서화 방법**

```javascript
# src/Components/Hello.js

import React from 'react';
import PropTypes from 'prop-types';

const Hello = ({ name, big, onHello, onBye }) => {
  return (
    <div>
      {big ? <h1>안녕하세요 {name}!</h1> : <p>안녕하세요 {name}!</p>}
      <div>
        <button onClick={onHello}>Hello</button>
        <button onClick={onBye}>Bye</button>
      </div>
    </div>
  );
};

Hello.propTypes = {
  /** 보여주고 싶은 이름 */
  name: PropTypes.string.isRequired,
  /** 이 값을 `true` 로 설정하면 h1 태그로 렌더링 됩니다. */
  big: PropTypes.bool,
  /** Hello 버튼 누를 때 호출할 함수 */
  onHello: PropTypes.func,
  /** Bye 버튼 누를 때 호출할 함수 */
  onBye: PropTypes.func,
};

Hello.defaultProps = {
  big: false,
};

export default Hello;

```

propTypes 를 설정 할 때 각 props 위에 /\*\* \*\*/ 주석으로 문구를 넣어주면 이 문구가 나중에 문서에서 나타나게 됨.

**실행 결과**

![storyboard-5](/assets/img/post/react/react-storyboard-5.PNG)

** 컴포넌트 부제목 및 설명 넣기**

parameters 추가

```javascript
# src/stories/Hello.stories.js

import React from 'react';
import Hello from '../Components/Hello';
import { withKnobs, text, boolean } from '@storybook/addon-knobs';
import { action } from '@storybook/addon-actions';

export default {
  title: 'components|basic/Hello', // 스토리북에서 보여질 그룹과 경로를 명시
  component: Hello, // 어떤 컴포넌트를 문서화 할지 명시
  decorators: [withKnobs], // 애드온 적용
  parameters: {
    componentSubtitle: '"안녕하세요"라고 보여주는 컴포넌트'
  }
};

export const hello = () => {
  // knobs 만들기
  const big = boolean('big', false, 'Group 1');
  const name = text('name', 'Storybook');
  return <Hello name={name} big={big} onHello={action('onHello')} onBye={action('onBye')} />;
};
hello.story = {
  name: 'Default',
};

export const standard = () => <Hello name="Storybook" />;
export const big = () => <Hello name="Storybook" big />;
```

설명추가

```javascript
# src/Components/Hello.js

/**
 * 안녕하세요 라고 보여주고 싶을 땐 `Hello` 컴포넌트를 사용하세요.
 *
 * - `big` 값을 `true`로 설정하면 **크게** 나타납니다.
 * - `onHello` 와 `onBye` props로 설정하여 버튼이 클릭했을 때 호출 할 함수를 지정 할 수 있습니다.
 */
const Hello = ({ name, big, onHello, onBye }) => {
  return (
```

**실행 결과**

![storyboard-6](/assets/img/post/react/react-storyboard-6.PNG)

#### MDX로 문서 작성하기

##### MDX는 언제 사용하는가?

Docs 애드온을 통하여 자동으로 만들어진 문서에서 제공하는 정보로는 컴포넌트의 기능을 자세하게 표현하기 어려운 상황에 MDX를 사용하면 된다.

(대부분의 경우, 자동으로 생성되는 문서만으로도 충분 할 때가 많다.)

추가적으로, 컴포넌트가 아닌 문서를 작성해야 하는 상황에는 (예: Introduction, Colors, Typography 등..) MDX-only로 작성하면 된다.

컴포넌트에 대한 MDX를 작성하실 때에는 MDX-only로 문서를 작성하는 것은 권장하지 않는다.

그 이유는 나중에 TypeScript를 사용하게 된다면 IDE에서 .mdx 확장자에 대한 TypeScript 지원이 제대로 이루어지지 않는다.

### Viewport

storyboard에서 반응형 구성 요소를 작성하고 확인할 수 있음.

#### Install

```
yarn -D @storybook/addon-viewport
```

#### Setting

.storybook/main.js에 '@storybook/addon-viewport/register' 추가

```
# .storybook/main.js

module.exports = {
  addons: ['@storybook/addon-viewport/register'],
};
```

# 참고자료

https://velog.io/@velopert/start-storybook

https://velog.io/@velopert/create-your-own-design-system-with-storybook
