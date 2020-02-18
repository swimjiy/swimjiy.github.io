---
slug: 2019-02-17-js-for
title:        "[JavaScript] forEach, for...in, for...of 정리"
description:     "for를 이용한 다양한 메서드들의 정의와 차이점을 알아보자."
date:         2019-02-17
published: true
banner: './js.jpg'
categories: [js]
tags:
    - js
    - ES6
    - for
---



### 세상은 넓고 for문의 종류도 많다. 

처음으로 시도해 본 코딩 테스트의 결과는 상당히 썼다. 글자를 읽을 수 있다고 해서 문맹률이 낮은 것은 아니라는 사실을 다시금 깨닫는 시간이었다. 그러나 포기하지 않으면 그 또한 과정이기에 지금부터 안되는 것을 되게 하는 노오력을 해 볼 예정이다. 그 첫 번째로 for문 정리 시작! :hatched_chick: 

 <br/>

### 클래식 for문

자바스크립트를 시작하면서 처음 접하는 메서드 중 하나가 `for문`이다. 흔히 알고 있는 클래식한 사용법은 다음과 같이 변수를 선언하고, 조건을 정하고, 증감식을 작성한다. 

```js
let foo = ["a", "b", "c"];

for (let i = 0; i < foo.length; i++){
    console.log(foo[i]);
}

// a, b, c
```

<br/>

### foEach문 

 ` forEach`문은 배열(Array)에서만 사용 가능한 메서드로, 배열의 각 요소들이 반복해서 작업을 수행할 수 있도록 돕는다. 또한 `item`이라는 콜백함수가 배열 내의 각 요소들의 값을 가리키고 있음을 알 수 있다.

```javascript
let arr = ["a", "b", "c"];

arr.forEach(function(i){
    console.log(i);
});

// a, b, c
```

<br/>

### for...in문

 `for...in` 문은 객체 내의 속성들을 반복하여 작업을 수행할 수 있다. 객체 내 `key`값에 접근할 수 있지만, `value`값에 직접적으로 접근하는 방법은 제공하지 않는다.

```javascript
let obj = {
    a: 1,
    b: 2,
    c: 3
};

for (let i in obj) {
    console.log(i + ': ' +obj[i]);
};

// a: 1, b: 2, c: 3
```

<br/>

### for...of

`for...of`는 ES6에서 새로이 추가된 구문이다. iterator 속성이 있는 객체 (`Array`, `Map`, `Set`,` String`, `TypedArray`, `arguments 객체` 등)의 값을 반복하며, `string` 과 같은 일반 문장형에도 loop가 가능하다.

```javascript
let arr = ["a", "b", "c"];

for (let i of arr) {
    console.log(i);
};

// a, b, c


let fruit = 'orange';

for (let i of fruit) {
    console.log(i);
};

// o, r, a, n, g, e
```

<br/>

### 그래서 차이점은?

가장 큰 차이점은 `for...in`은 **열거 가능한(enumerable) 속성이 true로 설정된 객체**들만 사용 가능하며, `for...of`는 **[Symbol.iterator] 속성이 있는 요소**에 대해 반복한다는 점이다. 가령 아까 `for...in`문에서 사용한 구문을 `for...of`에서 비슷하게 사용한다면 다음과 같은 결과가 나온다.

```javascript
let foo = {
    a: 1,
    b: 2,
    c: 3
};

for (let i of foo) {
    console.log(i);
};

// Uncaught TypeError: foo is not iterable
```

이는 `foo` 객체가 iterable속성이 없는 오브젝트 타입이기 때문에 발생한 에러이다. 그렇다면 반대로 `foo...of`문에서 사용한 구문을 `foo...in`에 적용한다면 어떤 결과가 나올까.



```javascript
let arr = ["a", "b", "c"];

for (let i in arr) {
    console.log(i);
};

// 0, 1, 2
```

아까와 달리 에러가 없긴 하지만, 배열의 value가 아닌 index값을 보여준다. 또한 for...in을 사용할 땐 다음과 같은 주의점이 있기 때문에 가급적 배열에서 사용하는 것은 지양하는 것이 좋다.



##### for...in 사용 시 주의점

- 순서가 보장되지 않는다. (프로퍼티 간에는 순서를 의식하지 않기 때문에 순서를 의식해야 하는 배열의 경우에는 for...in문을 사용하지 않는 것이 좋다.)
- length 사용 불가 (오브젝트의 경우 배열처럼 개수를 셀 수 없으므로 for...in문에서 오브젝트 내 키 값의 개수 등을 파악할 수 없다.)
- value값은 string이다. (연산작업을 할 수 없다.)

<br/>

## 결론

1. for를 이용한 반복문에는 클래식한 for문, forEach, for...in, for...of 등이 있다.
2. for...in은 오브젝트에서, for...of는 배열에서 사용하는 것이 좋다.

<br/>

## Reference

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

https://alligator.io/js/for-of-for-in-loops/

https://jsdev.kr/t/for-in-vs-for-of/2938