---
title: '[Node.js] Design Pattern'
date: 2020-03-22 18:00:00 -0400
categories: devlog
tags: nodejs devlog design
---

# Design Pattern

1. Functional Programming
2. OOP

# 함수형
데이터의 단방향 흐름

## example
```javascript
'use strict'

const numbers = [10, 20, 30, 40]

const sum = numbers.reduce((total, val) => total + val)

const avg = numbers.reduce((total, val, idx, arr) => {
    total +=val
    if(idx === arr.lenth-1) {
        return total/arr.length
    } else {
        return total
    }
    })
console.log(sum)
```

```javascript
'use strict'

const numbers = [0, 1, 2, 3, 4, 5, 6]

const res =numbers.reduce((total, amount) => {
if(amount > 0) total.push(amount)
return total 
}, [])

console.log(res)
```

```javascript
'use strict'

const arr = ['pdf', 'html', 'html', 'gif', 'gif', 'gif']

const res = arr.reduce((count, fileType)=> {
    count[fileType] = (count[fileType] || 0) +1
    return count
},{})

console.log(res);
```

# Singleton
어떠한 객체나 데이터에 대해 단일성, 최초 한번만 생성되는 것을 보장하는 패턴.

ex) 환경설정, Redis 캐시

## example
```javascript
'use strict'

'use strict'

class CacheManager {
    constructor() {
        if(!CaceManager.instance) {
            this._cache = []
            CacheManager.instance = this
        }
        return CacheManager.instance
    }
}

const instance = new CacheManager()
Object.freeze(instance)
```

# Adapter Pattern

클래스의 인터페이스를 사용자가 기대하는 다른 인터페이스로 반환하는 패턴

호환성이 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들이 함께 작동해주는 특징

```javascript
class AfricanLion {
    roar() {}
}

class AsianLion {
    roar() {}
}

class Hunter {
    hunt(lion) {
        lion.roar()
    }
}

class WildDog {
    bark() {}
}

//Adapter
class WildDogAdapter {
    constructor(dog) {
        this.dog = dog;
    }

    roar() {
        this.dog.bark();
    }
}

wildDog = new WildDog()
wildDogAdapter = new WildDogAdpter(wildDog)

hunter = new Hunter()
hunter.hunt(wildDogAdapter)
```

# Bridge Pattern

ex) 테마 적용 시

```javascript
class About {
    constructor(theme) {
        this.theme = theme
    }

    getContent() {
        return 'About page in' + this.theme.getColor()
    }
}

class Careers {
    constructor(theme) {
        this.theme = theme
    }

    getContent() {
        return "Careers page in " + this.theme.getColor()
    }
}

class DarkTheme {
    getColor() {
        return 'Dark Black'
    }
}

class LightTheme {
    getColor() {
        return 'Off white'
    }
}

class AquaTheme {
    getColor() {
        return 'Light blue'
    }
}

const darkTheme = new DarkTheme()

const about = new About(darkTheme)
const carreers = new Careers(darkTheme)

console.log(about.getContent())
console.log(careers.getContent())
```

# Decorator

주어진 상황 용도에 따라 책임을 덧붙이는 패턴

```javascript
class SimpleCoffee {
    getCost() {
        return 10
    }

    getDescription() {
        return 'Simple coffee'
    }
}

class MilkCoffee {

    constructor(coffee) {
        this.coffee = coffee
    }

    getCost() {
        return this.coffee.getCost() + 2
    }

    getDescription() {
        return this.coffee.getDescription() + ', milk'
    }
}

class WhipCoffee {
    constructor(coffee) {
        this.coffee = coffee
    }

    getCost() {
        return this.coffee.getCost() + 5
    }

    getDescription() {
        return this.coffee.getDescription() + ', whip'
    }
}

class VanillaCoffee {
    constructor(coffee) {
        this.coffee = coffee
    }

    getCost() {
        return this.coffee.getCost() + 3
    }

    getDescription() {
        return this.coffee.getDescription() + ', vanilla'
    }
}

let someCoffee

someCoffee = new SimpleCoffee();
console.log(someCoffee.getCost())
console.log(someCoffee.getDescription())

someCoffee = new MilkCoffee(someCoffee);
console.log(someCoffee.getCost())
console.log(someCoffee.getDescription())

someCoffee = new WhipCoffee(someCoffee);
console.log(someCoffee.getCost())
console.log(someCoffee.getDescription())

someCoffee = new VanillaCoffee(someCoffee);
console.log(someCoffee.getCost())
console.log(someCoffee.getDescription())
```

# Composite

객체들의 관계를 트리구조로 구성하여 부분 전체 계층을 표현하는 패턴.

사용자가 단일객체, 복합객체를 모두 다룰 수 있게 해줌.

```javascript
```