---
title: "[JavaScript] Performance"
date: 2019-12-24 18:00:00 -0400
categories: devlog
tags: javascript devlog
---


## 객체의 성능, 초기화 성능

성능을 생각하지 않고 작성하는 코드에 객체 선언과 초기화 구문이 있다.

### Array 형식의 객체와 Object형식의 객체를 생성 및 초기화하는 방법의 성능 비교

> 성능측정은 jsMatch

---

#### Array

- 객체 생성

  생성자 vs 리터럴

  ```javascript
  // 생성자를 사용한 배열 생성
  const arr = new Array();

  // 리터럴 형식으로 배열 생성
  const arr = [];
  ```

  **결과 : 큰 차이는 없으나 <span style="color:skyblue">리터럴 형식</span>을 사용할 경우 여러 브라우저에서 <span style="color:skyblue">좀더 좋은 성능</span>을 보임.**
  <br><br>

- 객체 초기화

  접근자 vs Push

  ```javascript
  // 접근자를 사용한 데이터 할당
  const arr = [];

  for (let i = 0; i < 1000; i++) {
    arr[i] = i;
  }

  // push()메소드를 사용한 데이터 핥당
  const arr = [];

  for (let i = 0; i < 1000; i++) {
    arr.push(i);
  }
  ```

  **결과 : <span style="color:lightcoral">크롬을 제외한</span> 대부분이 push법보다 <span style="color:skyblue">접근자</span>가 데이터를 할당하는 성능이 <span style="color:skyblue">2배 정도 더 빠르다.</span> (크롬은 push가 아주 미세하게 더 빠름)**

#### Object

- 객체 생성

  생성자 vs 리터럴

  ```javascript
  // 리터럴을 사용한 오브젝트 객체 생성
  const obj = {};

  //생성자를 사용한 오브젝트 객체 생성
  const obj = new Object();
  ```

  **결과 : 리터럴, 생성자 성능차이가 별로 없음.<br>
  이와 같이 성능 차이가 거의 없는 경우, 성능보다는 개발,유지보수,가독성까지 고려해서 코드 작성방법을 선택하는 것이 올바른 최적화 방법이다.**

- 객체 초기화

  연산자 vs []연산자

```javascript
// 연산자를 이용한 데이터 삽입
const obj = {};
obj.a =1;
obj.b =2;
...
obj.j=10;

// []연산자를 이용한 데이터 삽입
const obj = {};
obj["a"] = 1;
obj["b"] = 2;
obj["c"] = 3;
...
obj["j"] = 10;
```

**결과 : 객체의 초기화도 생성과 마찬가지로 한 가지 방식이 더 좋다고 판단할 수 없음.**

## 스코프 체인 탐색과 성능

> 스코프 체인이란?
>
> 자바 스크립트의 함수를 실행하면서 어떤 속성(변수, 객체 등)에 접근해야 할 때 해당 속성을 효율적으로 탐색하도록 속성을 일정한 객체 단위로 분류하고 각 객체에 접근하기 위한 객체의 참조를 특별한 공간에 저장해 둠. 이 공간이 스코프 체인이라 함.

JavaScript는 인터프리터 언어로 JIT(Just-In-Time)컴파일러 도입 등 실행을 최적화하기 위한 여러 가지 방법을 도입하고 있지만 개발자가 작성한 코드 자체의 성능이 런타임 성능에도 많은 영향을 줌.

런타임 환경에서 가장 많이 브라우저의 작업 가운데 자바스크립트의 실행 성능을 저해하는 요인이
 변수, 객체, 함수 등의 메모리상의 위치를 찾는 탐색 작업이 브라우저에서 어떻게 이뤄지는지 스코프 체인을 통해 알 수 있음.

#### 스코프 체인의 구성 요소
1. 활성화 객체 (Activation Object)
2. 전역 객체(Global Object)

## 반복문과 성능
for, for-in, while, do-while 구문에도 성능 차이가 있음.

## 효율적인 알고리즘 구현을 통한 성능

## 조건문과 성능

## 문자열 연산과 성능

## 정규표현식과 성능

-------

## 문법
### || 연산자
: 참을 만나면 그 뒤는 연산을 하지 않으므로 if문 대신 사용하면 코드량과 연산 횟수를 줄일 수 있다.

### && 연산자
참을 만나야 다음 연산을 하므로 어떤 조건을 만족할 때 실행하도록 하는 코드에서 사용하면 연산 횟수를 줄일 수 있다.

### double exclamation mark (!!)
!!표시를 사용하면 값의 유무를 판별 할 수 있다
```javascript
// 아래 경우를 제외하곤 true를 반환
!!false === false
!!0 === false
!!"" === false
!!null === false
!!undefined === false
!!NaN === false
```

### scope
자바스크립트는 블록내부에서 점차 큰 범위로 탐색한다. scope와 지역변수를 활용하면 성능 향상을 기대할 수 있다.

### innerHTML
innerHTML 횟수는 최소한으로 하는 것이 좋다.
브라우저는 갱신할 때마다 렌더링을 거치게 되기 때문이다.
(*브라우저가 웹을 그리는 법)

### 참조
참조 횟수를 최소한으로 줄이는 것이 좋다.
* 아래의 코드는 Clean Code에서 오래된 브라우저가 아니면 캐싱처리되어 상관없다고는 함.
```javascript
// loop를 돌 때마다 array 참조가 일어남.
for(let i=0; i < arr.length; i++) {
  ....
}
const l = arr.length;
for(let i=0; i < l; i++) {
...
}
```

### try/catch
try/catch 구문안에 있는 코드는 컴파일러가 최적화하지 못한다.
성능에 민감한 함수들은 도우미 함수를 생성하는 것이 좋다.
```javascript
function heler_func() {
  ....
}

try{
  ...
  helper_func();
  ...
} catch(e) {
  ...
}

## 이론
### 1. 지역변수를 정의하라
변수가 참조될 때, JavaScript는 Scope chain내의 다른 멤버들을 돌면서 해당변수를 찾습니다.
sopce Chain은 현재 scop내에서 사용 가능한 변수들의 모음이고, 대부분의 브라우저는 이것은 최소 두 가지 이상의 항목으로 구성하고 있다.
하나는 지역 변수들의 집합, 다른 하나는 전역변수들의 집합이다.

이 때 엔진이 탐색해야할 scope chain의 깊이가 깊을 수록, 작업 시간이 더 오래 걸리게 될 것이다.
엔진은 먼저 function의 인자인 this로 시작하는 지역변수들부터 찾는다.
그 다음에 지역적으로 정의된 변수들을 찾고, 그 후에 전역 변수들을 찾는 것을 반복합니다.
이 chain 내에는 지역변수가 우선이기 때문에 그들은 항상 전역 변수보다 더 빠르게 발견된다.
#### 결론 : 한 번 이상 전역변수를 사용할 때는 항상 지역적으로 재정의를 해야함.
```javascript
//ex
var blah = document.getElementById('MyID'), 
  blah2 = document.getElementById('myID2')

const doc = document, 
  blah = doc.getElementById('MyID'), 
  balh2 = doc.getElementById('MyID2');
```

### 2.with()문을 사용하지마세요
JavaScript엔진이 변수들을 돌 때, 먼저 with()변수들을 돌고, 다음에 지역 변수를 돌고, 다음으로 전역변수를 돌게 된다
본질적으로 with()는 지역변수들에게 전역변수가 갖는 모든 단점을 가지게 만든다.
JavaScript 최적화를 막는 요인이된다.

### 3.closure 사용을 아껴라.
