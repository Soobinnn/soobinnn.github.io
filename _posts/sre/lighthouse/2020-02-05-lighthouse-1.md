---
title: '[Lighthouse] Lighthouse (Audits)'
date: 2020-02-05 09:18:00 -0400
categories: sre
tags: lighthouse sre audits web
---

# Lighthouse 란?

웹 앱의 품질을 개선하는 오픈 소스 자동화 도구

Chrome 확장프로그램으로, Lighthouse에 확인할 URL을 지정하고 페이지에 대한 테스트를 실행한다음, 페이지에 대한 보고서를 생성한다.

# 특징

## 테스트 항목

75개 이상의 메트릭이 테스트하고 점수를 제공함.

- Performance

  time to interactive, 대기 시간, 속도 인덱스, 리소스 최적화, TTFB, asset delivery, 스크립트 실행 시간, DOM 크기 등등

- SEO

  모바일 친화적, meta, 크롤링, canonical, 구조 등

- Best Practices

  이미지 최적화, JS 라이브러리, 브라우저 오류 로깅, HTTPS를 통해 액세스 가능, 알려진 JS 취약성 등

- Accessibility

  페이지 요소, 언어, ARIA 속성 등

- PWA (Progressive Web Application)

  HTTP를 HTTPS로 리다이렉션, 응답 코드 양호, 3G에서의 빠른 로딩, 스플래시 화면, 뷰포트 등

# Install

[https://developers.google.com/web/tools/lighthouse?hl=ko](https://developers.google.com/web/tools/lighthouse?hl=ko)

# Start

사용 방법은 크게 3가지가 있다.

- web.dev
- 크롬 개발자도구에서 사용
- 확장프로그램으로 사용

> 100을 얻는데 너무 많은 시간을 소비하지말아야한다. Google 사이트 조차 100이 나오지 않는다. 그것을 지침으로 고려하여 최대한 향상 시키는 것이 중요하다.

## web.dev

[https://web.dev/measure/](https://web.dev/measure/)에서 URL 입력 - RUN Audit

\* web.dev는 모바일 장치를 사용하여 테스트를 실행한다.

![lighthouse-1](/assets/img/post/lighthouse/lighthouse-1.PNG)

![lighthouse-1-1](/assets/img/post/lighthouse/lighthouse-1-1.PNG)

## 크롬 개발자도구에서 사용

사용자 관점에서 실행

크롬 - F12 (개발자 도구) - Audits 탭 - Run

\* Chrome과 web.dev에서 사용하는 것은 비슷하, Chrome에서 실행할 경우, Progressive Web App라는 테스트 결과가 추가된다.

![lighthouse-2](/assets/img/post/lighthouse/lighthouse-2.PNG)

## 확장프로그램 사용

개발자 관점에서 사용

[설치 링크](https://developers.google.com/web/tools/lighthouse?hl=ko)

Node.js와 함께 사용하여 프로그래밍 방식으로 테스트 할 수 있다.

### Install

```
npm install -g lighthouse

# 설치 확인
lighthouse
```

### Start

```
lighthouse <URL> --chrome-flags="--headless"

```

실행하면 테스트 실행 결과보고서를 url경로로 생성된다. 기본적으로 PC에서 다운로드하거나 일부 웹 서버를 통해 제공 할 수 있는 HTML 형식의 보고서를 생성함.

#### JSON 형식으로 보고서를 생성하고 싶은경우

```
lighthouse <URL> --chrome-flags="--headless" --output json --output-path <URL>.json
```

[참고](https://github.com/GoogleChrome/lighthouse)

# 참고 문서

https://geekflare.com/google-lighthouse/
