---
slug: 2018-10-29-js-popup02
title:        "[JavaScript] Layer Pop-up02"
description:     "jQuery를 이용한 접근성 팝업 만들기"
date:         2018-10-29
published: true
banner: './js.jpg'
categories: [JavaScript, jQuery]
tags:
    - JavaScript
    - jQuery
    - Js
    - popup
---



가상의 팝업 공간을 만들고, 버튼을 클릭하면 버튼과 매칭되는 컨텐츠를 팝업 공간 안에 보여주는 팝업을 제작했다. 이 때 접근성을 고려하여 탭이 팝업창 안에서만 돌아갈 수 있도록 하는 함수를 추가했다.



### Markup

```html
<button class="btn-layer" data-layer-name="layer01">Pop-up</button>
<button class="btn-layer" data-layer-name="layer02">Pop-up</button>
<button class="btn-layer" data-layer-name="layer03">Pop-up</button>
<div class="layer" data-layer="layer01">
    <h3 class="layer-head">Title01</h3>
    <div class="layer-content">
        <a href="#">Link</a>
        <input type="text" placeholder="Input">
        <button>Button</button>
    </div>
</div>
<div class="layer" data-layer="layer02">
    <h3 class="layer-head">Title02</h3>
    <div class="layer-content">
        <a href="#">Link</a>
        <input type="text" placeholder="Input">
        <button>Button</button>
    </div>
</div>
<div class="layer" data-layer="layer03">
    <h3 class="layer-head">Title03</h3>
    <div class="layer-content">
        <a href="#">Link</a>
        <input type="text" placeholder="Input">
        <button>Button</button>
    </div>
</div>
```



### CSS

```css
* {
    margin: 0; 
    padding: 0;
}
.layer {
    display: none;
}
.layer-wrapper .layer {
    display: block; 
    position: absolute; 
    top: 0; 
    left: 0; 
    right: 0; 
    bottom: 0; 
    background-color: #fff;
}
```



### JavaScript

```javascript
$(function(){
    // 가상의 팝업 레이어를 생성한다.
    var $btn = $('.btn-layer');
    function createLayer(target){
        var $layer = target.clone();
        var $layerWrapper = $('<div class="layer-wrapper"/>');
        var $dim = $('<div class="dim" />')
        var $close = $('<button class="btn-layer-close">X</button>');
        $layer.attr('tabindex','0').append($close);
        $layerWrapper.append($dim).append($layer);
        $('body').append($layerWrapper);
        $('.layer-wrapper .layer').focus();
        layerFocusControl($('.layer-wrapper .layer'));
    };

    // 백탭, 탭을 실행했을 때 포커스가 레이어 팝업 영역 밖으로 벗어나지 않도록 제어하는 함수를 생성한다.
    function layerFocusControl(target){
        var $layer = target;
        var $firstEl = target.find('a, button, input, textarea, select, [tabindex="0"]').first();
        var $lastEl = target.find('a, button, input, textarea, select, [tabindex="0"]').last();
        $firstEl.on('keydown', function(e){
            if (e.keyCode == 9 && e.shiftKey){
                $lastEl.focus();
                e.preventDefault();
            }
        });
        $lastEl.on('keydown', function(e){
            if (e.keyCode == 9 && !e.shiftKey){
                $firstEl.focus();
                e.preventDefault();
            }
        });
    };

    // 버튼을 클릭했을 때 버튼과 매칭된 layer를 매개변수로 createLayer 함수를 실행한다.
    $btn.on('click', function(e){
        var $this = $(this);
        var layerName = $this.data('layerName');
        var $currentLayer = $('[data-layer ="' + layerName + '"]');
        e.preventDefault();
        $this.addClass('current-button');
        createLayer($currentLayer);
    });

    // 닫기 버튼을 클릭했을 때 생성된 레이어를 제거하고 이전에 클릭한 버튼에 포커스를 준다.
    $(document).on('click', '.btn-layer-close', function(e){
        var $this = $(this);
        var $layer = $this.parents('.layer-wrapper');
        var $currentBtn = $('.current-button');
        e.preventDefault();
        $layer.remove();
        $currentBtn.focus().removeClass('current-button');
    });
});
```







작업물은 추후에 정리해서 codepen에 업로드할 예정이다. 

