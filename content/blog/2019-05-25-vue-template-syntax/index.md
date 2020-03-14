---
slug: 2019-05-25-vue-template-syntax
title:        "[Vue.js] 템플릿 문법이란"
description:     "Vue에서 HTML 템플릿을 정의하는 방법"
date:         2019-05-25
published: true
banner: './vue.jpg'
categories: [Vue.js]
tags:
    - Vue
    - Vue.js
    - template
---



[Vue.js](<https://kr.vuejs.org/>)는 렌더링 된 DOM과 Vue 인스턴스의 데이터에 바인딩 할 수 있는 **HTML 기반의 문법**을 제공한다.

`Vue.js`는 내부적으로 템플릿 문법을 가상 DOM으로 리턴하는 render 함수로 컴파일 하는데, 이 떄 가상 DOM을 이용하여 최소한의 DOM을 조작하고 성능 부하를 최소화한다.

<br/>

------

<br/>

## 템플릿 문법1. 보간법 (Interpolation, 값 대입)

Vue 인스턴스에 있는 데이터를 HTML 템플릿에 표현하기 위해 사용한다.

콧수염을 닮은 Mustache {{ }} 템플릿 엔진을 사용하며, 가장 기본적인 데이터 바인딩 체계이다.

| Name                   | Code                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Text                   | ```<p> 메시지 : {{ msg }} </p><p *v-once*> 메시지 한 번만 : {{ msgOnce }} </p>``` |
| Raw HTML               | ```<p> Mustache: {{ blueMsg }} </p><p> v-html directive: <span *v-html*="blueMsg"> {{ blueMsg }} </span></p>``` |
| Attribute              | ```<p *v-bind*:*id* = "id"> ... </p>```                      |
| JavaScript 표현식 사용 | ```<p> {{ number }} + 1 = {{ number + 1 }} </p><img *v-bind*:*src* = "feel?smile:bad"/><p> Reverse : {{ *reverse**.**split*('')*.**reverse*()*.**join*('') }} </p>``` |

<br/>

## Text

{{  }} 사이에 변수 이름을 입력하면 해당 변수에 해당하는 데이터를 불러와 HTML 이스케이프로 출력된다. HTML 이스케이프란 특정 문자를 HTML로 변환하는 행위이며, `&lt;` 를 입력하면 `<`특수기호가 나오는 현상을 예로 들 수 있다. 

```vue
<p>메시지 : {{ msg }}</p>
```

데이터를 변경할 때 내용이 업데이트 되는 것을 막고 싶다면 `v-once` 디렉티브를 사용한다.

```vue
<p v-once>메시지 변경 금지 : {{ msg }}</p>
```

<br/>

### Raw HTML (원시 HTML)

Mustache 구문은 HTML이 아닌 일반 텍스트로 데이터를 해석하기 때문에 HTML 태그나 엔티티 기호 등이 데이터가 되면 그대로 출력된다. HTML 이스케이프로 출력해야할 경우엔 `v-html` 디렉티브를 사용한다.

```vue
<p> Mustache: {{ blueMsg }}</p>
<p> v-html directive: <span v-html="blueMsg"> {{ blueMsg }} </span></p>
```

<br/>

### Attribute

HTML 속성 (id, href, title, src 등...)은 Mustach 구문으로 데이터를 불러올 수 없기 때문에 `v-bind` 구문을 이용한다.

```vue
<p v-bind:id = "id">Attribute : This is my ID </p>
<a v-bind:href = "url">Attribute : This is URL</a>
```

<br/>

### JavaScript 표현식 

{{ }} 구문 안에서 자바스크립트의 모든 표현식 사용이 가능하다.

```vue
<p>{{ number }} + 1 = {{ number + 1 }}</p>
<p>If : {{ ok ? yes : no }}</p>
<p>Reverse : {{reverse.split('').reverse().join('')}}</p>
```

<br/>

------

<br/>

## 디렉티브(Directive)

디렉티브는 DOM을 제어하기 위한 지시(Directive) 로,  Vue에서는  `v- `접두어를 갖고 있으며 데이터의 값이 변경될 때, DOM을 반응적으로 변경하는 특별한 속성을 의미한다.

| Name   | Code                                                         |
| ------ | ------------------------------------------------------------ |
| v-if   | ```<p *v-if* = "seen"> 이제 나를 볼 수 있어요 </p>```        |
| v-bind | ```<a *v-bind*:*href* = "url">...</a><a :*href* = "url">...</a>``` |
| v-on   | ```<button *v-on*:*click* = "helloEvent"> … </button><button @*click* = "helloEvent"> ... </button>``` |
| 수식어 | ```<form *v-on*:*submit*.*prevent* = "onSubmit"> ... </form>``` |

<br/>

### v-if

`v-if`는 조건부의 true / false 여부에 따라 값을 표현한다. 

`v-show`와 기능이 비슷하지만, `v-show`의 경우 우선 렌더링이 되고 `display:block;` `display:none;` CSS 속성을 이용해 감추고 보여지는 반면 `v-if`는 제거되었다가 새로 생성된다.

따라서 `v-if`는 토글할 때의 비용이 높고, `v-show` 는 초기 렌더링 비용이 높으므로

자주 바뀐다면 `v-show`, 바뀌지 않는다면 `v-if` 를 권장한다.

```vue
<p v-show="seen">이제 나를 볼 수 있어요.</p>
<p v-if="type === 'A'">A</p>
<p v-else-if="type === 'B'">B</p>
<p v-else>Nothing</p>
```

<br/>

### v-bind

엘리먼트의 상태값을 바꿔줄 때 사용하는 디렉티브인데, 제이쿼리의 `attr`와 비슷한 역할로 볼 수 있다.

```vue
<a v-bind:href="url">네이버 링크</a>
<a :href="url">네이버 링크</a><!-- 약어 -->
```

<br/>

### v-on  

이벤트를 핸들링하는 디렉티브이며, 전달인자로 특정 이벤트를 받아 실행한다.

```vue
<button v-on:click="showAlert">Show Alert</button>
<button @click="showAlert">Show Alert</button><!-- 약어 -->
```

<br/>

### 전달인자

앞서 설명한 `v-bind`와 `v-on`와 같은 일부 디렉티브는 콜론 뒤에 부가적인 인자값을 작성할 수 있는데 이를 `전달인자`라고 부른다. 아래 예시의 `v-bind`의 경우 콜론(:) 뒤에 전달인자 `href`를 사용하여 반응적으로 HTML 속성값을 갱신한다. 

```vue
<a v-bind:href="url"...></a>
<a v-on:click="doSomething"> ... </a>
```

<br/>

### 수식어

점으로 표시되는 특수 접미사다.

가령 `<a>` 요소에는 개발자가 이벤트를 연결하지 않았음에도 특정 경로로 이동시키는 기능을 수행하는데 이를 `기본 이벤트`라고 한다. 이러한 기본 이벤트의 실행을 중지하기 위해 자바스크립트에서는 `preventDefault()` 이벤트 객체를 호출하는데, Vue에선 이벤트 수식어를 사용하여 이를 대신 호출할 수 있다.

```vue
<form v-on:submit.prevent="onSubmit"></form>
<!-- event.preventDefault()호출 -->
```

<br/>

### 약어

`v-` 접두사는 Vue 특정 속성을 구분하기 위한 시각적인 신호 역할이다. 그러므로 `v-` 접두어의 필요성이 떨어지거나 장황하다고 느낄 때, 약어를 사용한다.

```vue
<!-- 전체 -->
<button v-on:click="doSomething">...</button>
<!-- 약어 -->
<button @click="doSomething">...</button>

<!-- 전체 -->
<a v-bind:href="url">...</a>
<!-- 약어 -->
<a :href="url">...</a>
```

<br/>

------

<br/>

## Refer

[Vue.JS 공식 가이드](<https://kr.vuejs.org/v2/guide/syntax.html> )

[자바스크립트 프레임워크 소개 3 - Vue.js : TOAST Meetup]( <https://meetup.toast.com/posts/99>  )

[Vue.js 입문서 - 프론트엔드 개발자를 위한 : Captain Pangyo](<https://joshua1988.github.io/web-development/vuejs/vuejs-tutorial-for-beginner/>)

[리액트에 대해서 그 누구도 제대로 설명하기 어려운 것 – 왜 Virtual DOM 인가? : Velopert]( <https://velopert.com/3236> )

http://cigiko.cafe24.com/vue-js-%EB%B7%B0-%ED%85%9C%ED%94%8C%EB%A6%BF
https://takeuu.tistory.com/33
