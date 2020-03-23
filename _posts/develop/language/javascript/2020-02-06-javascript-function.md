---
title: '[JavaScript] Function'
date: 2020-02-06 13:39:00 -0400
categories: devlog
tags: javascript devlog function
---

## 문자열

### 소수점
- Math.ceil()
    소수점 올림, 정수 반환

- Math.floor()
    소수점 버림, 정수 반환

- Math.round()
    소수점 반올림, 정수 반환

- toFixed()
    원하는 소수점 길이만큼만 반올림하여서 반환

- toExponential()
    지정한 소수점 이하부터는 지수표기법으로 변환

- toPrecision()
    지정된 값만큼 반올림한 정수와 소수점

```javascript

const test = Math.floor();
~~test

```

## concat

두개의 문자열을 하나의 문자열로 만들어주는 역할을 하는 함수.

입력값을 문자열 대신 배열을 사용하면 두개의 배열을 하나의 배열로 만들어주는 역할도 함.

```
{String}.concat({String});
{Array}.concat({Array});

```

**\* push, concat 차이점**

> push()는 배열 끝에 요소를 추가하고 배열의 새길이를 반환한다. concat() 메소드는 배열을 병합하는데 사용된다. 기존 배열을 변경하지 않고 새 배열을 반환한다.

## push

## join

배열의 모든 요소를 연결해 하나의 문자열로 만듬.

## indexOf

## slice
배열 전체 혹은 부분 복제 할 때

## splice

기존 요소를 제거 하거나 새 요소를 추가하여 배열의 내용을 변경


```javascript
// 배열의 인덱스 0부터 2개를 제거, 그리고 그 자리에 'parrot', 'anemone' 를 삽입
removed = myFish.splice(0, 2, 'parrot', 'anemone');
```
## sort

배열의 요소를 적절한 위치에 정렬하고 배열을 반환
```javascript
var items = [10, 30, 2, 20];
// 오름차순
items.sort((a, b) => a - b);
console.log(items); // [2, 10, 20, 30]
// 내림차순
items.sort((a, b) => b - a);
console.log(items); // [30, 20, 10, 2]
// 이름의 길이순으로 정렬하기
var names = ['Kittie', 'John', 'Sally', 'Einstein'];
names.sort((a, b) => b.length - a.length);
console.log(names); // ['Einstein', 'Kittie', 'Sally', 'John']
```

## map


## reduce

# for

## for

## forEach

## mapv

## find

제공된 테스트 함수를 만족하는 배열의 첫 번째 요소를 반환

## findIndex

## some

## every

제공된 테스트 함수를 만족하는 배열의 첫 번째 요소에 대한 인덱스를 반환

# 참고 자료
https://mylife365.tistory.com/491