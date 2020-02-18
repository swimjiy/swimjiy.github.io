---
slug: 2018-07-08-javascript-study
title: "[JavaScript] JavaScript 기초 정리"
description: "객체 정리해둔 파일이 날아가버렸다. 추가예정"
categories: [JavaScript]
date:         2018-07-08
published: true
banner: './js.jpg'
tags: [JavaScript]
comments: true
---



## 선언문

내부 선언 방식

```html
<script>
자바스크립트 코드
</script>
```

외부 선언 방식

```html
<script src="자바스크립트 파일 경로"></script>
```



## 변수(Variables)

정의 : 변하는 수를 저장하는 공간

변수 선언 형식

```javascript
var 변수명 = 값;
var num = 100; //숫자형 데이터
var str = "hello"; //문자형 데이터
var bool = true; //논리형 데이터
```



## 연산자

정의 : 프로그래밍 계산 작업에 필요한 부호
자세한 내용은 [msdn](https://msdn.microsoft.com/ko-kr/library/6hsc0eak(v=vs.94).aspx) 참조



| 종류             | 내용                                                         |
| ---------------- | ------------------------------------------------------------ |
| 산술 연산자      | +, -,*, /, %(나머지)                                         |
| 문자결합 연산자  | +(산술과 쓰임새는 다름)                                      |
| 대입 연산자      | 오른쪽 피연산자의 값을 왼쪽 피연산자에 대입, +=, -=, *=, %=  |
| 증감 연산자      | ++, -- (숫자형 데이터를 1씩 증감)                            |
| 비교 연산자      | 두 데이터의 값을 비교, >, <, >=, <=, ==, !=, ===, !== (뒤에 두 개는 데이터타입까지 비교) |
| 논리 연산자      | \|\|(or), &&(and), !(not)                                    |
| 삼항 조건 연산자 | 조건식 ? 실행문1 : 실행문2; (true일 땐 실행문1, false일 땐 실행문2 출력) |



## 제어문

정의 :  프로그램의 흐름을 제어할 수 있도록 도와주는 실행문

#### 1. 조건문

- if문 , else if문 (조건 만족 여부에 따라 스크립트 코드 수행 여부가 결정)

```javascript
if (조건식1) {
	실행문1;
} else if (조건식2){
    실행문2;
} else {
    실행문3;
}
```

#### 2. 선택문

- switch문 (일치하는 경우에 값이 있을 경우 선택하여 수행)

```javascript
var 변수 = 초기값;
switch (변수) {
	case 값1: 실행문1;
	break;
	case 값2: 실행문2;
	break;
	default : 기본값;
}
```

#### 3. 반복문

- while문 (조건식을 만족하는 동안 반복실행)

```javascript
var 변수 = 초기값;
while (조건식) {
	실행문;
	증감식;
}
```

- do while문 (반드시 한 번은 실행문을 실행하고 조건식을 검사)

```javascript
var 변수 = 초기값;
do {
    실행문;
    증감식;
}
while (조건식)
```

- for문 (while과 방식은 동일)

```javascript
for (초기값; 조건식; 증감식){
    실행문;
}
```



## 함수

정의 : 데이터만 저장할 수 있는 변수와는 달리, 일련의 실행문을 메모리에 저장하고 호출할 수 있는 공간.



## 함수 선언문

```javascript
function add(a+b){
    return a+b;
} // 선언 함수

var add = function(a,b){
    return a+b;
} // 익명 함수
```



## 함수 호출

```javascript
function 함수명(매개변수1, 매개변수2...매개변수n){
    스크립트 실행문;
}

함수명(데이터1[인자], 데이터2...데이터n); //함수 호출
```

> 매개변수가 없을 때는 괄호를 빈 값으로 두고 함수명(); 으로 진행하면 된다.



#### 내장함수의 종류

| 종류         | 설명                                                         |
| ------------ | ------------------------------------------------------------ |
| parseInt()   | 문자형 데이터 -> 정수형 데이터 ("5.12" -> 5)                 |
| parseFloat() | 문자형 데이터 -> 실수형 데이터 ("5.12" -> 5.12)              |
| String()     | 문자형 데이터로 변경                                         |
| Number()     | 숫자형 데이터로 변경                                         |
| Boolean()    | 논리형 데이터로 변경                                         |
| isNaN()      | 데이터에 숫자가 아닌 문자를 포함하면 true 반환 "5-3" -> false |
| eval()       | 문자형 데이터를 큰따옴표가 없는 스크립트 코드로 처리 "15+5" -> 20 |



#### return문

정의 : 함수에서 결과값을 되돌려줄 때 사용

유형 : 데이터 반환, 강제종료, 재귀 함수 호출

```javascript
function calc(){
    var result = 100+200;
    return result; //데이터를 반환하는 return문
}

function myFnc(){
    document.write("hello");
    return; // 함수를 강제 종료하는 return문
    document.write("javascript");
}  -> 결과 : hello

function testFnc(){
    num++;
    document.write(num);
    if(num==10) return; //정의문 내에서 함수를 다시 호출하는 return문
    -> 결과 : 12345678910
}
```



#### 지역 변수와 전역 변수

전역 변수

```javascript
var 변수;
function 함수명(){
    변수=값;
}
```

지역 변수

```javascript
function 함수명(){
    var 변수=값;
}
```



## 이벤트

정의 : 브라우저에서 방문객이 취하는 모든 동작을 이벤트라고 한다. 또한 이벤트가 발생했을 때 자바스크립트 실행문을 실행하는 것을 이벤트 핸들러라 일컫는다.



### 이벤트 종류

- 마우스 이벤트

| 종류        | 설명                                   |
| ----------- | -------------------------------------- |
| onmouseover | 지정한 요소에 마우스가 들어갔을 때     |
| onmouseout  | 지정한 요소에 마우스가 벗어났을 때     |
| onmousemove | 지정한 요소에 마우스가 움직였을 때     |
| onclick     | 지정한 요소를 마우스로 클릭했을 때     |
| ondbclick   | 지정한 요소를 마우스로 더블클릭했을 때 |



- 키보드 이벤트

| 종류       | 설명                                                         |
| ---------- | ------------------------------------------------------------ |
| onkeypress | 모든 키를 눌렀으며 실제로 글자가 써질 때 (shift, enter같은 키는 인식하지 못한다) + onkeydown이 일어나고 나서 인식된 값을 가져옴. |
| onkeydown  | 모든 키를 눌렀을 때 (shift, alt, control 등의 키도 인식)     |
| onkeyup    | 모든 키를 눌렀다 뗐을 때 (인식  키는 down과 동일)            |



- 기타 이벤트

| 종류     | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| onfocus  | 포커스가 들어갔을 때                                         |
| onblur   | 포커스가 다른 요소로 이동되어 잃었을 때                      |
| onchange | 지정한 요소에 value 값이 바뀌고 포커스가 이동되었을 때 ex) select박스 |
| onload   | 지정한 요소의 하위요소를 모두 로딩했을 때                    |
| onunload | 문서를 닫거나 다른 요소로 이동했을 때                        |
| onsubmit | 폼 요소에 전송버튼을 눌렀을 때                               |
| onreset  | 폼 요소에 취소버튼을 눌렀을 때                               |
| onresize | 지정된 요소의 크기가 변경되었을 때                           |
| onerror  | 문서 객체가 로드되는 동안 문제가 발생할 때                   |



### 이벤트 선언 방식

- 직접 요소 이벤트 등록 방식

```html
<button id="btn" onclick="alert('Event')">버튼</button>
```



- DOM을 이용한 이벤트 등록 방식

```html
<button id="btn">버튼</button>

document.getElementId('btn').onclick = function(){
    alert('Event');
}
```



### 키보드 접근성

마우스가 없거나 시각장애인과 같이 마우스 사용이 어려운 경우에도 이벤트가 작동할 수 있도록 하는 것.

가령 ```onmouseover``` 는 ```onfocus``` 와 함께 사용해주거나 ```onmouseout```은 ```onblur``` 와 함께 작성해야 한다.



### 이벤트 중복 등록

한 요소에 중복으로 이벤트를 등록하게 될 경우,  일반적으로는 맨 마지막에 있는 이벤트만 실행하고 나머지 이벤트는 실행하지 않는다. 이러한 중복 이벤트 문제를 해결하기 위해 이벤트 등록 메서드를 사용할 수 있다.

```javascript
요소 선택.addEventListener("이벤트 종류", 함수명 또는 익명함수, false(표준 캡처 방식));
//일반 브라우저

요소 선택.attachEvent("on이벤트 종류",함수명 또는 익명 함수);
// ie8 이하
```



### this 키워드

정의 : 방문자가 이벤트를 발생한 요소



### 이벤트 객체

정의 : 사이트에 방문자가 지정한 요소에서 이벤트가 발생한 경우, 이벤트 핸들러(익명 함수)에 이벤트 객체를 생성하여 실행문으로 사용 가능

- ie9이상 이벤트 객체 생성

```html
<script type="text/javascript">
	document.onkeydown=function(e){
        alert(e);
	}
</script>
```

- ie8이하 이벤트 객체 생성

```html
<script type="text/javascript">
	document.onkeydown=function(e){
        alert(window.event);
	}
</script>
```

- 모든 브라우저 호환 (삼항조건연산자를 이용, true면 e 실행, false면 window.event 실행)

```html
<script type="text/javascript">
	document.onkeydown=function(e){
        var eventObj = e?e:window.event;
        alert(eventObj);
	}
</script>
```



#### 이벤트 객체 속성 종류

- 마우스 이벤트 객체 속성

| 종류    | 설명                                                         |
| ------- | ------------------------------------------------------------ |
| clientX | 마우스 이벤트가 발생한 X 좌푯값 (수평 스크롤바 이동 너비 무시) |
| clientY | 마우스 이벤트가 발생한 Y 좌푯값 (수평 스크롤바 이동 높이 무시) |
| pageX   | 마우스 이벤트가 발생한 X 좌푯값 (수평 스크롤바 이동 너비 포함) |
| pageY   | 마우스 이벤트가 발생한 Y 좌푯값 (수평 스크롤바 이동 높이 포함) |
| screenX | 화면 모니터를 기준으로 이벤트가 발생한 X 좌푯값              |
| screenY | 화면 모니터를 기준으로 이벤트가 발생한 Y 좌푯값              |
| layerX  | position을 적용한 요소를 기준으로 이벤트가 발생한 X 좌푯값   |
| layerY  | position을 적용한 요소를 기준으로 이벤트가 발생한 Y 좌푯값   |
| button  | 마우스에 눌린 버튼의 값                                      |

- 키보드 이벤트 객체 속성

| 종류     | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| keyCode  | 키보드에 눌린 유니코드 값                                    |
| altKey   | ```alt``` 키가 눌려 있으면 true를, 그렇지 않으면 false를 반환합니다. |
| ctrlKey  | ```ctrl``` 키가 눌려 있으면 true를, 그렇지 않으면 false를 반환합니다. |
| shiftKey | ```shift``` 키가 눌려 있으면 true를, 그렇지 않으면 false를 반환합니다. |

- 전체 이벤트 객체 속성

| 종류   | 설명                                            |
| ------ | ----------------------------------------------- |
| target | this와 같이, 이벤트가 발생한 요소를 반환합니다. |



### 참고 서적

+ [Do it! 자바스크립트 + 제이쿼리 입문](http://www.aladin.co.kr/shop/wproduct.aspx?ItemId=44282289)