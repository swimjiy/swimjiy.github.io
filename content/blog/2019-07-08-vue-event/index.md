---
slug: 2019-07-08-vue-event
title:        "[Vue.js] 이벤트 핸들링"
description:     "v-on 디렉티브를 이용한 다양한 핸들링 방법"
date:         2019-07-08
published: true
banner: './vue.jpg'
categories: [Vue.js]
tags:
    - Vue
    - Vue.js
    - event
---



[vue.js](<https://kr.vuejs.org/>)에서는 `v-on`디렉티브를 사용하여 다양한 이벤트 핸들링 방법을 지원한다.

<br/>

### 1. 기본 이벤트 핸들링

`v-on:click="counter += 1"` 처럼 직접 자바스크립트 코드를 적을 수도 있고, 아래와 같이 메소드의 이름을 받아 핸들링할 수 있다.

```html
<div id="example-2">
  <button v-on:click="greet">Greet</button>
</div>
```

```javascript
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  methods: {
    greet: function (event) {
      alert('Hello ' + this.name + '!')
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})
```



#### 1-1. 매개변수 지정

매개변수를 지정하여 메소드에 값을 전달할 수 있다.

```html
<div id="example-3">
  <button v-on:click="say('hi')">Say hi</button>
  <button v-on:click="say('what')">Say what</button>
</div>
```

```javascript
new Vue({
  el: '#example-3',
  methods: {
    say: function (message) {
      alert(message)
    }
  }
})
```



#### 1-2. DOM이벤트에 접근

 `$event` 변수를 사용해 원본 DOM이벤트에 접근할 수 있다.

```html
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>
```

```js
methods: {
  warn: function (message, event) {
    if (event) event.preventDefault()
    alert(message)
  }
}
```

<br/>

### 2. 이벤트 수식어

Vue.js에서는 `v-on` 이벤트에 이벤트 수식어를 제공한다. 이벤트 수식어란  `event.preventDefault()` 또는 `event.stopPropagation()`와 같은 복잡한 자바스크립트 구현을 간단히 처리할 수 있는 수식어로, 점(.)으로 표시된 접미사다.

| 이벤트 수식어 | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| `.stop`       | `.stopPropagation()`과 동일. 클릭 이벤트 전파가 중단.        |
| `.prevent`    | `.preventDefault()`과 동일. 제출된 이벤트가 페이지를 다시 로드하지 않음. |
| `.capture`    | 내부 엘리먼트를 대상으로 하는 이벤트가 해당 엘리먼트에서 처리되기 전에 동작. |
| `.self`       | event.target이 엘리먼트 자체인 경우에만 트리거를 처리        |
| `.once`       | 이벤트가 최대 한번만 트리거 되게 함.                         |
| `.passive`    | `.prevent`의 반대. 기본 이벤트를 취소할 수 없다.             |

<br/>

### 3. 키 수식어

키 이벤트를 수신할 때 `v-on`에 대한 키 수식어를 추가할 수 있다.

```html
<input v-on:keyup.13="submit">
```



위의 예시처럼 키코드를 직접 입력할 수도 있고, 아래의 키 수식어 별칭을 이용할 수도 있다.

키 수식어와 동일하게 마우스 버튼에 대한 수식어도 사용할 수 있다.

| 키 수식어 명 | 고유 키 값 |
| ------------ | ---------- |
| `.enter`     | 13         |
| `.tab`       | 9          |
| `.delete`    | 8          |
| `.esc`       | 27         |
| `.space`     | 32         |
| `.up`        | 33         |
| `.down`      | 34         |
| `.left`      | 37         |
| `.right`     | 39         |

```html
<input v-on:keyup.enter="submit">
```



#### 3-1. 시스템 수식어 키

시스템 수식어 키를 이용해 해당 키가 눌러진 경우에만 마우스 또는 키보드 이벤트 리스너를 트리거할 수도 있다.

| 시스템 수식어 키 |
| ---------------- |
| `.ctrl`          |
| `.alt`           |
| `.shift`         |
| `.meta`          |

```html
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```



#### 3-2. 사용자 지정 키 수식어

또한 전역 `config.keyCodes` 객체를 통해 사용자 지정 키 수식어 별칭을 지정할 수 있다.

```javascript
Vue.config.keyCodes.f1 = 112
```



#### 3-3. `.exact`

`.exact`는 다른 키와 같이 눌리지 않고 지정된 키만 정확하게 눌렀을 때 이벤트가 실행되게 한다.

```html
<!-- Alt 또는 Shift와 함께 눌린 경우에도 실행. -->
<button @click.ctrl="onClick">A</button>

<!-- Ctrl 키만 눌려있을 때만 실행. -->
<button @click.ctrl.exact="onCtrlClick">A</button>
```

<br/>

### 4. 마우스 버튼 수식어 

키 수식어와 동일하게 마우스 버튼에 대한 수식어도 사용할 수 있다.

| **마우스 버튼 수식어명** |
| ------------------------ |
| `.left`                  |
| `.right`                 |
| `.middle`                |

```html
<button v-on:mouseover.left="alert">Alert</button>
<button @mouseover.left="alert">Alert</button>
```

<br/>

### Refer

[Vue.js 공식 문서 - 이벤트 핸들링](<https://kr.vuejs.org/v2/guide/events.html>)

