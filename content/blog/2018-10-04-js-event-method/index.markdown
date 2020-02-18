---
slug: 2018-10-04-js-event-method
title:      "[JavaScript] e.preventDefault / e.stopPropagation"
description:   "이벤트를 제어하는 메서드"
date:       2018-10-05
published: true
banner: './1004_thumb.png'
tags:
    - e.preventDefault
    - e.stopPropagation
    - JavaScript
---



## e.stopPropagation

e.stopPropagation는 이벤트의 전파 또는 전달을 막는 메서드이다.  이 메서드의 존재 이유에 대해 알고자 한다면 먼저 이벤트가 전파/전달된다는 특성에 대해 짚고 나가는 것이 좋다.

자바스크립트로 어떤 DOM에 이벤트를 실행시켰을 때, 이벤트는 우리가 지정해놓은 특정 엘리먼트에만 적용되지 않고 해당 엘리먼트의 자식, 부모 엘리먼트까지 전파된다. 이 때 최초의 엘리먼트에서 부모 요소로 전파되는 방식을 버블링 (Bubbling), 자식 요소로 전달되는 방식을 캡쳐링 (Capturing) 이라고 정의한다.

![버블링 캡쳐링 도식화](./1004_thumb.png)

```html
<body onclick="onClick(this);">body
    <div onclick="onClick(this);">div
        <p onclick="onClick(this);">p
            <button onclick="onClick(this);">button</button>
        </p>
    </div>
    
    <script type="text/javascript">
        function onClick(element, e) {
            e = window.event || e;
        }
    </script>
</body>
```

![버블링 결과](./1004_img01.png)

이 상태로 button 엘리먼트를 클릭하게 되면 버블링으로 button의 상위 엘리먼트인 p, div, body까지 이벤트가 실행된 것을 볼 수 있다.

![e.stopPropagation 결과](./1004_img02.png)

e.stopPropagation는 이러한 이벤트 버블링, 캡쳐링을 방지하기 위해 호출한다. 이벤트 함수 안에 e.stopPropagation를 추가하고 실행한 결과는 다음과 같다.



```html
<body onclick="onClick(this);">body
    <div onclick="onClick(this);">div
        <p onclick="onClick(this);">p
            <button onclick="onClick(this);">button</button>
        </p>
    </div>

    <script type="text/javascript">
        function onClick(element, e) {
            e = window.event || e;
            console.log(element.nodeName);
            
            // e.stopPropagation 추가
            e.stopPropagation();
        }
    </script>
</body>
```



이처럼 의도치않은 버블링, 핸들링을 막기 위해서 자주 사용되는 메서드이므로 이벤트 핸들링에 있어 참고해 두자.



## e.preventDefault

e.preventDefault는 이벤트의 기본 동작이 호출되지 않도록 막는 역할을 한다.  이 메서드의 역할을 설명하기 가장 좋은 예시로 ```a``` 태그가 있다.

a는 기본적으로 원하는 위치로 이동할 수 있는 앵커 기능이 있다.  이 때 href="#" 속성을 넣어주게 되면 a를 클릭할 때 페이지 최상단으로 이동하게 되는데, 이는 a의 기본 동작이기 때문에 a 안에  이벤트가 추가되었을 때에도 마찬가지로 적용된다. 그 결과는 사용자의 불편함을 초래한다.

이 때 아래와 같이 이벤트 함수 안에  e.preventDefault();를 추가하게되면 이벤트 호출 시 a의 기본 동작을 막아줌으로써 원하지 않은 최상단으로의 이동을 방지할 수 있다. 

```html
<script type="text/javascript">
    function onClick(e) {
        alert('hello');
        e.preventDefault();
    }
</script>
```



## 결론

이상 이벤트 핸들러와 관련된 메서드들을 알아보았다. 다른 사람들의 코드를 보면 자주 사용하는것을 볼 수 있었는데 어떤 상황에서 쓰면 되는지만 알고 그 원리에 대해서는 자세히 몰랐기 때문에 이번 기회를 통해 정리해봤다. 미처 다루지 못한 메서드들은 앞으로 공부하면서 계속 추가할 예정이다.