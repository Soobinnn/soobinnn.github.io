---
title: '[Node.js] Express.js'
date: 2020-03-02 09:57:00 -0400
categories: devlog
tags: nodejs devlog express
---

# Express.js 란?

Node.js의 핵심 모듈인 http와 Connect 컴포넌트를 기반으로 하는 웹 프레임워크

미들웨어라고 하며, 설정보다는 관례와 같은 프레임워크

Node.js를 위한 빠르고 간편한 웹 프레임워크

## 작동 방식

메인 파일이라고 하는 진입점이 있다.

컨트롤러, 유틸리티, 도우미, 모델과 같은 자체적인 모듈을 비롯하여 서드파티 의존 모듈을 include 한다.

템플릿 엔진과 해당 템플릿 엔진의 파일 확장자와 같은 Express.js 앱 설정을 구성한다. 오류 핸들러, 정적 파일 폴더, 쿠키 및 기타 파서와 같은 미들웨어를 정의함. 라우팅 정의 및 DB와 연결한다.

## Express 기본 구조

```
express
|______package.json
|______public
|       |______css
|       |______style.css
|______router
|       |______main.js
|______server.js
|______views
|       |______about.html
|       |______index.html
```

## Doc

```javascript
// 현재 디렉토리
__dirname;

// 상대적인 경로로 연결
path.resolve('/foor/bar', './bar');
```

# 참고 자료

https://github.com/expressjs
