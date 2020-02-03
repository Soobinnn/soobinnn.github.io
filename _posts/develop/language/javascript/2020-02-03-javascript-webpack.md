---
title: '[JavaScript] WebPack'
date: 2020-02-03 10:54:00 -0400
categories: devlog
tags: javascript devlog webpack
---

# WebPack 이란?

코드의 양이 많아지면 코드의 유지와 보수가 쉽도록 코드를 모듈로 나누어 관리하는 모듈 시스템이 필요해짐.

그러나 JavaScript 언어 자체가 지원하는 모듈 시스템이 없다.

이러 한계를 극복하려 여러 가지 도구를 활용하는데 그 도구중 하나가 Webpack.

JavaScript 모듈화 명세를 만드는 대표적인 작업 그룹

1. [CommonJS](http://www.commonjs.org/)
2. [AMD (Asynchronous Module Definition)](https://github.com/amdjs/amdjs-api/wiki/AMD)

**WebPack은 두 그룹의 명세를 모두 지원하는 JavaScript 모듈화 도구**

모듈 번들러는 여러개의 자바스크립트 파일을 하나의 파일로 묶어서 한번에 요청을 통해 가져올 수 있게 하고 최신 자바스크립트 문법을 브라우저에서 사용할 수 있게해줌.

물론, 수 많은 자바 스크립트 파일이 하나의 파일로 묶인다면 초기 로딩 속도가 어마어마해짐.

모듈 번들러들은 이런 문제를 해결하기 위해 청크, 캐시, 코드 스플릿 개념을 도입하여 문제를 해결하고 있음.

# 적용

1. 리액트 프로젝트에 적용
2. 자바스크립트 프로젝트에 적용

## 리액트 프로젝트에 적용

```
yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader clean-webpack-plugin css-loader html-loader html-webpack-plugin mini-css-extract-plugin node-sass react react-dom sass-loader style-loader webpack webpack-cli webpack-dev-server
```

## 자바스크립트 프로젝트에 적용

# 참고 문서

https://d2.naver.com/helloworld/0239818

https://velog.io/@jeff0720/React-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%9D%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%A9%B4%EC%84%9C-%EB%B0%B0%EC%9A%B0%EB%8A%94-Webpack-%EA%B8%B0%EC%B4%88
