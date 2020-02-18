---
slug: 2019-01-30-css-grid-2
title:        "[CSS] grid 레이아웃 정리 (2) 자식 요소"
description:     "CSS3 grid 레이아웃의 정의 및 부모 요소 속성 정리"
date:         2019-01-30
published: true
banner: './css.jpg'
categories: [CSS]
tags:
    - CSS
    - grid
---



## 자식 요소 속성

#### ** Notice

`float`, `display: inline-block`, `display: table-cell`, `vertical-align`, `column-*` 속성은 그리드 자식 요소에서 적용되지 않으므로 주의한다.



### 1. grid-column-start/end  |  grid-row-start/end

grid 자식 요소의 열 위치를 지정한다. `grid-column-start` 와 `grid-row-start` 는 행과 열의 시작을, `grid-column-end` 와`grid-row-end`는 행과 열의 끝을 정의한다. 

속성값으로는 숫자 혹은 부모 요소 css에서 지정한 라인 이름 등이 들어올 수 있다.

```css
.item {
    grid-column-start: <숫자> | <이름> | span <숫자> | span <이름> | none;
    grid-column-end: <숫자> | <이름> | span <숫자> | span <이름> | none;
    grid-row-start: <숫자> | <이름> | span <숫자> | span <이름> | none;
    grid-row-end: <숫자> | <이름> | span <숫자> | span <이름> | none;
}
```



#### span?

grid에서는 자식 요소에는 span이라는 특수한 함수를  사용할 수 있다. 이는 **특정 위치로부터 n번째 값**을 일컫는데, 기존에 `grid-column: 2 / 3` 이 2열부터 3열까지를 의미한다면 `grid-column: 2 / span 3` 은 2열부터 2열에서 3번째로 떨어진 값을 의미하므로 5열을 뜻함을 알 수 있다.

직접 값을 입력해보면 다음과 같다.

<script async src="//jsfiddle.net/sumim/c5bxrs4j/19/embed/html,css,result/"></script>

<br/>

### 2. grid-column  |  grid-row

1번의 속성에서  `grid-column-start` + `grid-column-end` ,  `grid-row-start` + `grid-row-end`  으로 묶어놓은 축약형 속성이다. 

```css
.item {
    grid-column: <column-start> / <column-end>;
    grid-row: <row-start> / <row-end>;
}
```

<br/>

### 3. grid-area

`grid-area`는 두 가지 방법으로 사용할 수 있다. 첫 번째는 `grid-column`과 `grid-row`의 축약형, 두 번째는 부모 요소 속성인 `grid-template-areas` 의 속성자로 필요한 셀 이름 지정이 있다.

```css
.item {
    grid-area: <이름> | <row-start> / <column-start> / <row-end> / <column-end>
}
```

<br/>

#### 3-1.  `grid-column`과 `grid-row`의 축약형

<script async src="//jsfiddle.net/sumim/c5bxrs4j/24/embed/html,css,result/"></script>

<br/>

#### 3-2. 셀 이름 지정

셀 이름을 지정함으로써 부모 요소 속성인 `grid-template-areas` 의 속성자로 사용이 가능하다.

```css
.container {
    grid-template-area: 
        "header haeder header"
        "aside main main"
        "footer footer footer";
}
.item {
    grid-area: header;
}
```

위의 경우엔 부모 요소의 header에 해당되는 부분이 .item의 영역이 되는 것이다.

<br/>

## 결론

이번에는 grid 레이아웃의 정의 및 사용방법에 대해 알아보았다. 나조차도 처음 접해본 속성이기 때문에 설명에 미숙한 부분도 있었고 포스트를 작성하면서 새롭게 알게 된 사실도 있었다. 따라서 부족한 예제 및 설명은 하단 **Reference**에 추가하고 틈틈히 공부할 계획이다.

<br/>

## Reference

https://css-tricks.com/snippets/css/complete-guide-grid/

https://gridbyexample.com/