---
title: '[JavaScript] 문법'
date: 2020-02-06 17:01:00 -0400
categories: devlog
tags: javascript devlog function
---

## Map

## Set

## Hoisting

자바스크립트에서 실행 context. 실행 단계가 어떻게 동작하는가에 대한 일반적인 생각

변수 및 함수선언은 컴파일 단계에서 메모리에 저장되지만 자바스크립트가 어떤 코드 구문을 실행하기 전에 함수선언을 메모리에 저장하는 특징

### Example
```javascript
// 일반적인 방법
// 선언 후 호출하는 방법
function say(word) {
	consol.log(word)
}
say('hi');

// Hoisting의 특징
//자바스크립트가 어떤 코드 구문을 실행하기 전에 함수 선언을 메모리에 저장하는 특징 때문에
//코드에서 선언하기 전에 함수를 사용할 수 있다.
say('hi')
function say(word) {
	consol.log(word)
}
```

## IIFE 

즉시 실행 함수 표현

정의 되자마자 즉시 실행되는 자바스크립트 함수
```javascript
(function() {
	// 전역 스코프에 불필요한 코드 방지
	// 다른 변수들이 접근하는 것을 막음
	var lang = 'js';
})();

console.log(lang);
```

## Binding

함수 호출과 실제 함수를 연결하는 방법.

함수를 호출하는 부분에 함수가 위치한 메모리 번지를 연결 시켜 주는 것.

자바스크립트에서 함수를 호출 할 때는 암묵적으로 arguments객체 및 this변수가 함수 내부로 전달된다.

이에 따라 this에 할당되는 값이 달라지게 된다.

### Binding Rule

1. 객체의 메소드 호출 할 때 this 바인딩
2. 함수를 호출 할 때 this 바인딩
3. 생성자 함수를 호출 할 때 this 바인딩
4. call, apply 메소드를 이용한 명시적 바인딩

#### 1. 객체의 메소드 호출 할 때 this 바인딩

객체 내부의 함수를 메소드라 부른다.

메소드 내부 코드에서 사용된 this는 해당 메소드를 호출한 객체로 바인딩된다.

```javascript
var myObject = {
	name: 'foo',
	sayName: () => {
		console.log(this.name);
	}
};

var otherObject = {
	name: 'bar'
};

otherObject.sayName = myObject.sayName;

myObject.sayName(); // foo
otherObject.sayName(); // bar
```

ES6의 화살표 함수는 this를 자체적으로 바인딩하지 않는다.

화살표 함수를 사용하면 별도로 binding을 해주지 않고도 사용 가능하다.

#### 2. 함수를 호출 할 때 this 바인딩

함수를 호출할 경우는, 해당 함수 내부 코드에서 사용된 this는 전역 객체에 바인딩 된다.

브라우저에서 자바스크립트를 실행하는 경우 전역 객체는 widnow 객체다.

```javascript
var test = 'This is test';
console.log(window.test); // 'This is test'

var sayFoo = () => {
	console.log(this.test);
};

sayFoo(); // 'This is test'
```

내부 함수를 호출 했을 경우데 동일하다.

내부 함수들은 함수로 취급되어 this는 전역 객체에 바인딩 된다.

```javascript
var value = 100;

var myObject = {
	value: 1,
	func1: () => {
		this.value += 1;
		console.log('func1() called. this.value : ' + this.value); // 2, 호출한 객체의 this가 바인딩
		// func1 내부 함수 func2
		func2 = () => {
			this.value += 1;
			console.log('func2() called. this.value : ' + this.value); // 101, 내부함수로서, 전역객체에 binding 된다.

			//func2의 내부 함수 func3
			func3 = () => {
				this.value += 1;
				console.log('func3() called. this.value : ' + this.value); // 102
			};
			func3();
		};
		func2();
	}
};

myObject.func1();
```

그래서 that변수를 이용해 this값을 저장한다.

```javascript
var value = 100;

var myObject = {
	value: 1,
	func1: () => {
		var that = this; // 현재 바인딩 된 this(myObject)를 that에 저장

		this.value += 1;
		console.log('func1() called. this.value : ' + this.value); // 2,
		// func1 내부 함수 func2
		func2 = () => {
			that.value += 1;
			console.log('func2() called. this.value : ' + that.value); // 3
		};
		func2();
	}
};

myObject.func1();
```

#### 3. 생성자 함수를 호출 할 때 this 바인딩

기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다. 생성자 함수에서의 this는 생성자 함수를 통해 새로 생성되어 반환되는 개체에 바인딩된다.

#### 4. call과 apply 메소드를 이용한 명시적인 바인딩

Function.prototype 객체의 메서드인 call() 과 apply()를 통해 명시적으로 this를 바인딩 가능하다.

```javascript
function.apply(thisArg, argArray)
```

call() 과 apply()의 기능은 함수 호출이다. thisArg는 this에 바인딩 할 객체, argArray는 함수를 호출 할 때 넘길 인자들의 배열이다.

```javascript
function Person(name, age) {
	this.name = name;
	this.age = age;
}

var applyPerson = {};
var newPerson = new Person('mike', 24);

Person.apply(applyPerson, ['Jack', 24]);

console.log(applyPerson.name); // Jack
console.log(newPerson.name); // call
```

## Arrow Function (화살표 함수)

function 키워드를 사용해서 함수를 만든 것보다 간단히 함수를 표현 할 수 있다.

화살표 함수는 항상 익명이다.

```javascript
// 일반 함수
var foo = function() {console.log("foo")};

// 화살표 함수
var bar = () => console.log("bar);

// 일반 함수
function add (var1, var2) {
	return var1 + var2
}

// 화살표 함수
const add = (var1, var2) => var1 + var2
```

### 일반함수 , 화살표 함수

일반함수가 전역 컨텍스트에서 실행될 때 this가 정의함.

화살표 함수는 this를 정의하지 않음.

#### 화살표 함수 선언방법

```javascript
// 매개변수 지정 방법
    () => { ... } // 매개변수가 없을 경우
     x => { ... } // 매개변수가 한 개인 경우, 소괄호를 생략할 수 있다.
(x, y) => { ... } // 매개변수가 여러 개인 경우, 소괄호를 생략할 수 없다.

// 함수 몸체 지정 방법
x => { return x * x }  // single line block
x => x * x             // 함수 몸체가 한줄의 구문이라면 중괄호를 생략할 수 있으며 암묵적으로 return된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.

() => {           // multi line block.
  const x = 10;
  return x * x;
};
```

#### 일반함수

```javascript
let cat = {
	sound: 'meow',
	soundPlay: function() {
		console.log(this); // 가.
		setTimeout(function() {
			console.log(this); // 나.
			console.log(this.sound); // 다.
		}, 1000);
	}
};

cat.soundPlay();
// 가. cat {sound: "meow", soundPlay: ƒ}
// 나. window
// 다. undefined -----> undefined인 이유는 window에 sound가 없어서입니다.
```

일반함수에서 적절한 this를 전달하는 방법

```javascript
// 함수안에 that 변수를 선언하기
let cat = {
	sound: 'meow',
	soundPlay: function() {
		let that = this; // that 사용
		setTimeout(function() {
			console.log(that.sound);
		}, 1000);
	}
};

cat.soundPlay();
// 1초 후에 ... "meow"

// bind 사용하기
let cat = {
	sound: 'meow',
	soundPlay: function() {
		setTimeout(
			function() {
				console.log(this.sound);
			}.bind(this),
			1000
		); // bind 사용
	}
};

cat.soundPlay();
// 1초 후에 ... "meow"
```

#### 화살표 함수

```javascript
let cat = {
	sound: 'meow',
	soundPlay: function() {
		setTimeout(() => {
			console.log(this.sound);
		}, 1000);
	}
};

cat.soundPlay();
// 1초 후에 ... "meow"
```

#### 비교 예제 2

일반 함수

```javascript
function Prefixer(prefix) {
	this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
	return arr.map(
		function(x) {
			return this.prefix + ' ' + x;
		}.bind(this)
	); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Soo', 'Bin']));
```

화살표 함수

```javascript
function Prefixer(prefix) {
	this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
	return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Soo', 'Bin']));
```

#### 비교 예제3
```javascript
// 일반함수
API.prototype.get = function(resource) {
	var self = this;
	return new Promise(function(resolve, reject) {
		http.get(self.uri + resource, function(data) {
			resolve(data);
		})
	})
}

// 화살표 함수
API.prototype.get = (resource) =>
	new Promise((resolve, reject) => {
		http.get(this.uri + resource, (data) => {
			resolve(data);
		})
	})
```

### example
```javascript
const getDiscount = (price, rate) => price * rate

// f(x) = x + 1
// g(x) = x^2
// h(x) = f(g(x))
const getDiscount = rate => price => rate * price

const getTenpercentOff = getDiscount(0.1)(10000)

const getTenpercentOff = getDiscount(0.1);

getTenpercentOff(10000)

var getDiscount = function getDiscount(rate) {
	return function (price) {
		return rate * price;
	}
}
```

## Destructuring assignment (구조 분해 할당)

### 구조 분해

좌측 :값을 넣을 변수

우측 : 값이되는 변수

```javascript
var a, b, rest;
[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2

[a, b, ...rest] = [1, 2, 3, 4, 5];
console.log(a); // 1
console.log(b); // 2
console.log(rest); // [3, 4, 5]

({ a, b } = { a: 1, b: 2 });
console.log(a); // 1
console.log(b); // 2
```

### 배열 구조 분해

```javascript
const foo = ['one', 'two', 'three'];
const [one, two, three] = foo;

console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"

const array = ['dog', 'cat', 'sheep'];
const [first, second] = array;
console.log(first, second); // dog cat
```

## Generator
### 정의
사용자의 요구에 따라 다른 시간 간격으로 여러 값을 반환할 수 있으며, 내부 상태를 관리할 수 있는 함수.

단 한 번의 실행으로 함수의 끝까지 실행이 완료되는 일반 함수와는 달리 일시적으로 정지될 수 있고, 다시 시작될 수도 있다.

generator는 화살표 함수로 선언하지 않고 명시적으로 선언해야함.

Generator 함수는 generator를 반환한다. 

Generator는 iterable, iterator를 따르는 객체이다.

- yield 

Generator 함수 실행을 일시적으로 정지시키며, yield 뒤에 오는 표현식은 Generator의 caller에게 반환된다.
즉, 일반 함수의 return과 매우 유사하며

여기서 제너레이터 함수는 Call이고, 이를 호출 하는 함수가 Caller이며,
Caller는 Call의 yield 부분에서 다음 statment로 진행 할 지 여부를 제어한다. 



### Example
```javascript
'use strict'

// yield 
// 함수를 끝내지 않고 반환한다.
// return

function* log () {
	console.log(0, yield);
	console.log(1, yield);
	console.log(2, yield);
}

const gen = log()

gen.next('zero')
gen.next('first')
gen.next('second')

const obj = {
		*gen() {
			let cnt = 0;
			yield ++cnt;
			yield ++cnt;
			yield ++cnt;
		}
}

const g = obj.gen()
console.log(g.next())
console.log(g.next())
console.log(g.next())
```


# 참고 자료

https://velog.io/@litien/Javascript-This-Binding

https://hanjungv.github.io/2018-02-03-1_JS_arrow_function/

https://wonism.github.io/javascript-generator/