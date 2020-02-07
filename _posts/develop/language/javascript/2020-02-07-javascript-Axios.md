---
title: '[JavaScript] Axios'
date: 2020-02-07 14:23:00 -0400
categories: devlog
tags: javascript devlog Axios
---

# Axios 란?

Axios는 HTTP 클라이언트 라이브러리, 비동기 방식으로 HTTP 데이터 요청을 실행함.

직접적으로 XMLHttpRequest를 다루지 않고 "AJAX 호출"을 할 수 있다.

Promise기반의 API형식. Axios는 브라우저, Node.js에서 모두 사용 가능. IE8이상을 포함한 최신 브라우저 지원

## Fetch Api 보다 좋은 이유

1. 구형 브라우저 지원
2. 요청을 중단 시킬 수 있음.
3. 응답 시간 초과를 설정하는 방법이 있음
4. CSRF 보호 기능이 내장됨.
5. JSON 데이터 자동변환
6. Node.js에서 사용가능

## Install

```
npm install axios

yarn add axios
```

## Start

### Basic

axios({옵션})

```javascript
axios({
	url: 'https://v1/api/wancs/board',
	method: 'get',
	data: {
		name: '임수빈'
	}
});
```

### Method

보기 명확하게 method를 분리하여 사용할 수 있음.

- axios.get()
- axsios.post()
- axios.delete()
- axios.patch()
- axios.option()

#### GET

axios.get('URL주소').then().catch()

```javascript
axios.get('https://test.com/?foo=bar');

axios.get('https://test.com/', {
	params: {
		foo: 'bar'
	}
});
```

#### POST

axios.post('URL주소').then().catch()

```javascript
axios.post('https://test.com');
```

```javascript
axios.post('https://test.com/', {
	params: {
		foo: 'bar'
	}
});
```

# 참고 문서

https://github.com/axios/axios
