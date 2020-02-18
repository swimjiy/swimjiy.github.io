---
slug: 2019-06-06-vue-lifecycle
title:        "[Vue.js] 라이프사이클과 훅"
description:     "라이프사이클과 자주 사용하는 훅을 알아보자"
date:         2019-06-06
published: true
banner: './vue.jpg'
tags:
    - Vue
    - Vue.js
    - lifecycle
---



## 라이프사이클이란

어떤 Vue 인스턴스가 생성되면, 미리 사전에 정의된 몇 가지 단계를 거치게 되는데 이를 **라이프사이클(Life Cycle)** , 번역하면 **생명주기** 라고 부른다. 다시 말해, 라이프사이클이란 Vue 인스턴스가 생성(Create), 부착(Mount), 갱신(Update), 소멸(Destroy)의 4가지 단계를 거치는 과정을 뜻한다.



## 라이프사이클 훅

라이프사이클의 특정 시점에서 원하는 로직을 수행하기 위해서 라이프사이클 훅(Lifecycle Hook)을 이용한다. 가장 많이 사용하는 훅으로는 `beforeCreate`, `Created`, `beforeMount`, `mounted`, `beforeUpdate`, `updated`, `beforeDestroy`, `destroyed` 총 8개가 있다.



## 라이프사이클 다이어그램

Vue.js 공식 문서에서 제공하는 다이어그램이며, 라이프사이클의 전반적인 흐름을 한 눈에 확인할 수 있다.

![vue라이프사이클 다이어그램](https://kr.vuejs.org/images/lifecycle.png)

### beforeCreate

가장 처음 실행되는 훅이며, 이벤트 및 라이프사이클이 초기화된 후 사용한다. 



### Created

반응성 및 주입 기능을 추가한 뒤 사용한다. 이 단계에서 인스턴스는 데이터 처리, 계산된 속성, 메서드, 감시/이벤트 콜백 등과 같은 옵션 처리를 완료한다.



### beforeMount

beforeMount는 el, template 속성이 컴파일되고, template의 내용을 render()로 변환한 뒤에 호출된다. 



### Mounted

vm.$el 이 생성되고 el의 속성 값을 대체한 이후에 호출된다. Mount 단계 이후이기 때문에 렌더링된 DOM에 접근할 수 있다.



### beforeUpdate

데이터가 변경되고, 가상 DOM이 재 렌더링되고 패치되기 전에 호출된다. 재 렌더링 전의 데이터를 확인할 수 있으며 더 많은 상태 변경이 가능하다.



### Updated

데이터가 변경되고, 가상 DOM이 재 렌더링되고 패치까지 완료하면 호출된다. DOM이 업데이트가 된 상태에서 접근할 수 있기 때문에 DOM에서 종속적인 연산이 가능하다.



### beforeDestroy

Vue 인스턴스가 제거되기 전에 호출된다. 따라서 아직까지 인스턴스에 접근이 가능하며, 컴포넌트는 원래 모습과 모든 기능들을 그대로 가지고 있다.



### Destroyed

Vue 인스턴스가 제거된 후에 호출된다. Vue 인스턴스의 모든 디렉티브가 바인딩 해제되고, 모든 이벤트 리스너가 제거되며 모든 하위 Vue 인스턴스도 삭제된다.



## Example Code

```vue
// Lifecycle.vue

<template>
    <div id="root">
        <h1>Lifecycle State : {{ msg }}</h1>
    </div>
</template>
<script>
export default {
    data() {
        return{
            msg: 'View Lifecycle'
        }
    },
    beforeCreate() {
        this.msg = 'beforeCreate'
        console.log('beforeCreate')
    },
    created() {
        this.msg = 'created'
        console.log('created')
    },
    mounted(){
        this.msg = 'mounted'
        console.log('mounted')
    },
    updated(){
        this.msg = 'updated'
        console.log('updated')
    },
    destroyed(){
        this.msg = 'destroyed'
        console.log('destroyed')
    }
}
</script>
```



## Refer

[Vue 인스턴스 — Vue.js]([https://kr.vuejs.org/v2/guide/instance.html#%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%ED%9B%85](https://kr.vuejs.org/v2/guide/instance.html#인스턴스-라이프사이클-훅))

[라이프사이클 훅 — Vue.js]([https://kr.vuejs.org/v2/api/#%EC%98%B5%EC%85%98-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%ED%9B%85](https://kr.vuejs.org/v2/api/#옵션-라이프사이클-훅))

[Instance Lifecycle — Cracking Vue.js](https://joshua1988.github.io/vue-camp/vue/life-cycle.html#%EB%9D%BC%EC%9D%B4%ED%94%84-%EC%82%AC%EC%9D%B4%ED%81%B4-%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8)

