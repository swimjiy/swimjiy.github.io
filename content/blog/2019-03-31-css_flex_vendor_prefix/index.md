---
slug: 2019-03-31-css_flex_vendor_prefix
title:        "CSS flex 벤더 프리픽스 정리"
description:     "버전별 flex 호환 코드 정리"
date:         2019-03-31
published: true
banner: './css.jpg'
categories: [CSS]
tags:
    - CSS
    - flex
    - vendorprefix
---



현재 진행 중인 앱 프로젝트에서 안드로이드 4.3 젤리빈에서 CSS `flex` 속성이 먹히지 않는 이슈가 발생했다.  

*우리 모두 하위 버전을 멀리합시다!*

미리 알아두어야 할 점은 현재 우리가 흔히 사용하고 있는 `flex`는 2012년에 정의된 명세이며, 이와 약간 사용법이 다른 2009년 명세가 존재한다는 것이다.

찾아보니 안드로이드 2.1 ~ 4.3 버전에서는 2009년의 `flex` 명세를 지원하기 때문에 `webkit` 벤더 프리픽스를 붙이고 2009년 버전의 `flex` 를 입력해야 한다고 한다.

따라서 이번 이슈를 해결할 겸 버전별 flex 벤더 프리픽스 코드를 정리했다.

<br/>

## 컨테이너 적용 속성

### flex 설정

```css
.container {
    display: -webkit-box | -webkit-inline-box; /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    display: -moz-box | -moz-inline-box; /* Firefox 19- */
    display: -ms-flexbox | -ms-inline-flexbox; /* IE10 */
    display: -webkit-flex | -webkit-inline-flex; /* Chrome */
    display: flex | inline-flex;
}
```

<br/>


### 주축

기존 `flex-direction` 이 `column-reverse` 처럼 주축과 역순 여부를 동시에 설정할 수 있었다면, 하위 버전에서는 `box-orient` 와 `box-direction` 으로 주축과 역순 여부를 분리하여 설정한다는 점에 주의한다.

```css
.container {
    -webkit-box-orient: horizontal | vertical; /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    -webkit-box-direction: normal | reverse; /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    -moz-box-orient: horizontal | vertical; /* Firefox 19- */
    -moz-box-direction: normal | reverse; /* Firefox 19- */
    -ms-flex-direction: row | column | row-reverse | column-reverse; /* IE10 */
    -webkit-flex-direction: row | column | row-reverse | column-reverse; /* Chrome */
    flex-direction: row | column | row-reverse | column-reverse;
}
```

<br/>

### 줄바꿈

맨 앞에 있는 속성값이 기본값이다.

```css
.container {
    -webkit-box-lines: single | multiple; /* ios 6-, safari 3.1-6 */
    -moz-box-lines: single | multiple; /* Firefox 19- */
    -ms-flex-wrap: none | wrap | wrap-reverse; /* IE10 */
    -webkit-flex-wrap: nowrap | wrap | wrap-reverse; /* Chrome */
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

<br/>

### 아이템 가로 정렬

 `space-between` 는 `justify` 로 대응할 수 있으나  `space-around` 는 일치하는 2009년 속성값이 없으므로 사용에 유의한다.

```css
.container {
    -webkit-box-pack: start | end | center | justify;
    /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    -moz-box-pack: start | end | center | justify; /* Firefox 19- */
    -ms-flex-pack: start | end | center | justify; /* IE10 */
    -webkit-justify-content: flex-start | flex-end | center | space-around | space-between;
    /* IE10 */
    justify-content: flex-start | flex-end | center | space-around | space-between; /* Chrome */
}
```

<br/>

### 아이템 세로 정렬

```css
.container {
    -webkit-box-align: start | end | center | stretch | baseline;
    /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    -moz-box-align: start | end | center | stretch | baseline; /* Firefox 19- */
    -ms-flex-align: start | end | center | stretch | baseline; /* IE10 */
    -webkit-align-items: flex-start | flex-end | center | stretch | baseline; /* IE10 */
    align-items: flex-start | flex-end | center | stretch | baseline; /* Chrome */
}
```

<br/>

## 아이템 적용 속성

### 크기

```css
.item {
    -webkit-box-flex: 1; /* Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 */
    -moz-box-flex: 1; /* Firefox 19- */
    -ms-flex: 1; /* IE10 */
    -webkit-flex: 1; /* Chrome */
   	flex: 1;
}
```

<br/>

### 정렬 순서

2009년 명세는 양의 정수, 2012년 명세는 정수를 속성값으로 쓸 수 있다.

```css
.item {
	-webkit-box-ordinal-group: 1; /* ios 6-, safari 3.1-6 */
	-moz-box-ordinal-group: 1; /* Firefox 19- */
	-ms-flex-order: 0; /* IE10 */
	-webkit-order: 0; /* Chrome */
	order: 0;
}
```

<br/>

## 결론

세부적으로는 차이가 존재하지만 크게 정리해보자면 아래의 표와 같다.


| Version                                 | Vendor Prifix                 |
| --------------------------------------- | ----------------------------- |
| Android 2.1 ~ 4.3, ios 6-, safari 3.1-6 | -webkit- 접두사 + 2009년 명세 |
| Firefox 19-                             | -moz- 접두사 + 2009년 명세    |
| IE10                                    | -ms- 접두사 + 2009년 명세     |
| Chrome                                  | -webkit- 접두사 + 2012년 명세 |
| 기타 최신 버전                          | 없음                          |

개인적으로 정리한 내용으로 결함이 있을 수 있으며, 이슈 대응 뒤 정리한 내용과 다른 점이 생기면 수정할 예정이다.

<br/>

## References

https://css-tricks.com/using-flexbox
https://m.blog.naver.com/cihjl/221318653767
https://ptb2.me/flexbox