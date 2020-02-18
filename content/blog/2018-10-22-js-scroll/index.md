---
slug: 2018-10-22-js-scroll
title:        "[jQuery] Scroll Event"
description:     "jQuery를 이용한 스크롤 이벤트 만들기"
date:         2018-10-22
published: true
banner: './js.jpg'
categories: [JavaScript, jQuery]
tags:
    - JavaScript
    - jQuery
    - scroll
---



jQuery 메서드를 이용하여 원하는 위치로 스크롤을 이동시키는 이벤트를 만들었다. 이벤트를 만드는데 충족시킨 기본 조건은 아래와 같다. 



### 조건

1. 버튼 및 섹션 컬러 설정
2. 버튼을 클릭하면 매칭된 div 위치로 스크롤 이동
3. 스크롤을 내릴 때 화면에 노출된 div와 일치한 버튼 컬러 변경
4. 스크롤이 최상단에서 일정 높이까지 내려갔을 때 버튼 바 컬러 전체 변경
5. title 버튼에 마우스가 진입했을 때 애니메이션 진행





##### 버튼 및 섹션 컬러 설정


```javascript
var colors = ['orange', 'yellow', 'green', 'blue', 'purple'];
var btnColors = ['#fff', 'gray', 'pink'];
$('.section').each(function(i, obj){
	$(this).css('background-color', colors[i]);
});
$('ul>li button').css('background-color', btnColors[0]);
$('.button').eq(0).css('background-color', btnColors[2]);
```



##### 버튼을 클릭하면 매칭된 div 위치로 이동

```javascript
$('.button').each(function(i, obj){
    $(this).on('click', function(){
        var section = $('.section').eq(i);
        $('html, body').stop().animate({scrollTop: section.offset().top - 50}, 500);
    });
});
```



##### 스크롤을 내릴 때 화면에 노출된 div와 일치한 버튼 컬러 변경

##### 스크롤이 최상단에서 일정 높이까지 내려갔을 때 버튼 바 컬러 전체 변경

```javascript
$(window).scroll(function(){
    var windowTop = $('html, body').scrollTop();
    $('.section').each(function(i){
        var headerHeight = $('.header').height() + 1;
        var sectionTop = $(this).offset().top;
        var hight = $(this).height();
        if (windowTop + headerHeight > sectionTop && windowTop + headerHeight <= sectionTop + hight){
            $('.button').css('background-color', btnColors[1]);
            $('.button').eq(i).css('background-color', btnColors[2]);
        } else if (windowTop < 50) {
            $('ul>li button').css('background-color', btnColors[0]);
            $('.button').eq(0).css('background-color', btnColors[2]);
        }
    });
});
```



##### title 버튼에 마우스가 진입했을 때 애니메이션 진행

```javascript
$('#button01').mouseenter(function(){
    var $this = $(this).find('span');
    $this.stop().animate({
        top: '-100%'  
    }, 300, function(){
    $this.stop().animate({
        top: '100%'
        }).stop(true, true).animate({
          top: '0'
        },600);
    });
});
```





## 결과

<p data-height="365" data-theme-id="dark" data-slug-hash="QZBKYE" data-default-tab="js,result" data-user="sumim00" data-pen-title="Window scroll animation" class="codepen">See the Pen <a href="https://codepen.io/sumim00/pen/QZBKYE/">Window scroll animation</a> by Sumim (<a href="https://codepen.io/sumim00">@sumim00</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>



codepen 홈페이지랑 브라우저에서는 잘 나오는 것 같은데 상단의 codepen editor로 확인하면 마지막 section에서 버튼이랑 조금 애매하게 틀어지는 것 같다. height값이 미묘하게 안맞는 것 같은데 확인해봐야겠다.