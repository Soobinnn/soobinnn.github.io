---
title: '[JavaScript] moment.js'
date: 2020-03-09 10:13:00 -0400
categories: devlog
tags: javascript devlog moment
---

# moment.js

장점 : 시간계산이 편하다.

단점 : 무겁다.

### format()

```javascript

moment("MM-DD-YYYY").format();
moment("YYYY/MM/DD HH:mm:ss").format();
```

###  subtract
```javascript
moment().subtract(5,'minutes')
moment().subtract(24,'hours')
moment().subtract(1,'days')

```

### startOf('String')
시작을 0으로 맞춰줄 때 사용

```javascript

moment().startOf('day');
moment().startOf('week');
moment().startOf('moment');
moment().startOf('year');
```
### endtOf('String')
```javascript

moment().endtOf('day');
moment().endOf('week');
moment().endOf('moment');
moment().endOf('year');
```

# Tip
```javascript
function timeForToday(value) {
        const today = new Date();
        const timeValue = new Date(value);

        const betweenTime = Math.floor((today.getTime() - timeValue.getTime()) / 1000 / 60);
        if (betweenTime < 1) return '방금전';
        if (betweenTime < 60) {
            return `${betweenTime}분전`;
        }

        const betweenTimeHour = Math.floor(betweenTime / 60);
        if (betweenTimeHour < 24) {
            return `${betweenTimeHour}시간전`;
        }

        const betweenTimeDay = Math.floor(betweenTime / 60 / 24);
        if (betweenTimeDay < 365) {
            return `${betweenTimeDay}일전`;
        }

        return `${Math.floor(betweenTimeDay / 365)}년전`;
 }

```

# 참고 문서

https://velog.io/@wo0kgod/Moment-js%EB%A1%9C-%EC%8B%9C%EA%B0%84%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A1%B0%EC%9E%91%ED%95%98%EA%B8%B0