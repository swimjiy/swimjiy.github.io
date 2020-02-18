---
slug: 2018-10-08-add-disqus-comment
title:      "[Disqus] 블로그 댓글 기능 추가하기"
description:   "Disqus 서비스를 이용해 쉽게 댓글 기능을 추가해보자"
date:       2018-10-08
published: true
banner: './disqus_thumb.jpg'
tags:
    - Disqus
    - jekyll
    - github
    - blog
    - comment
---



## 서론

Disqus란 2007년에 만들어진 소셜 댓글 서비스로 다양한 소셜 네트워크의 사람들이 서로 생각을 공유할 수 있도록 만들어진  도구이다. 회원가입 후 api를 연동시키기만 하면 개인 블로그에 빠르고 쉽게 댓글 기능을 달 수 있기 때문에 전세계의 수많은 블로거들의 사랑을 받고 있다. 

github blog처럼 정적 블로그를 사용하면 원하는대로 커스텀할 수 있다는 장점이 있긴 한데, 나같이 귀찮음이 온몸에 밴 사람들에겐 그 장점이 바로 단점으로 돌아온다...

지금 사용하고 있는 Jekyll 테마는 기본으로 disqus가 적용되어 있긴 한데 새 블로그로 이전할 때를 대비해서 추가 방법을 정리해보고자 한다.





## 시작

![disqus 회원가입](./disqus_01.png)

먼저 [Disqus 홈페이지](https://disqus.com/) 에 들어가 get start 버튼을 누르면 회원가입 폼이 생성된다. 양식대로 작성하고 회원가입을 진행하면 된다. 

![disqus 이용 목적 선택 창](./disqus_02.png)

Signup 버튼을 누르고 회원가입이 완료되면 이런 창이 뜬다. 상단 버튼은 사이트에 코멘트를 달 것인지 묻는 내용이므로 하단의 내 블로그에 Disqus 설치하기 버튼을 누른다.

![적용할 사이트 입력](./disqus_03.png)

**Website Name**에  댓글 기능을 넣고자 하는 사이트 url을 추가하고 **Crate Site** 버튼을 클릭한다. 





## 플랫폼 선택

![disqus 댓글 기능 선택](./disqus_04.png)

사용할 댓글 기능을 고르는 화면인데 나는 무료로 사용하는 Basic을 선택했다. 

![disqus 댓글 기능 선택](./disqus_05.png)

클릭하고 나면 내 블로그에서 사용하는 플랫폼을 선택하는 창이 나타난다. 나는 Jekyll을 사용하고 있기 때문에 Jekyll을 선택했다.

![disqus 댓글 기능 선택](./disqus_06.png)

그럼 이제 내 블로그에 Disqus를 설치할 수 있는 방법이 나타난다. 





## 코드 추가

1. ```_posts ``` 디렉토리 안에 있는 포스트 파일의 YAML 머리말에 ``` comments: true ``` 변수를 추가한다.

   ```
   layout: post
   title: JavaScript 클래스 단위 프로그래밍
   date:         2018-08-18 18:55:00
   author:       "Sumim"
   header-img:   "https://sumim00.github.io/img/in-post/post-thumb/2018-08-18.jpg"
   header-mask:  0.3
   tags: [JavaScript, 자바스크립트]
   comments: true
   ```


2. 2번이라고 쓰여져 있는 부분을 보면 Universal Embed Code를 확인할 수 있는데, 클릭하면 추가될 부분에 아래와 같은 코드가 나타단다. 이 코드를 블로그 실행 시에 댓글창이 나타날 영역에 추가하면 되는데 이 때 두 가지 방법을 사용할 수 있다.



   + disqus코드만 있는 파일을 따로 생성한 뒤 레이아웃 파일에 ```{% if page.comments %}```와 ```{% endif %}``` 태그를 추가하고, 그 사이에 생성한 파일명 삽입
   + 레이아웃 파일에 직접 Universal Embed Code를 추가



   둘 중에 본인이 원하는 방법을 사용하면 된다. 내 경우는 ```_layouts ``` 폴더 안에 이미 추가가 되어있어서 이 작업은 빼고 진행했다. 



   ![disqus shorname 확인](./disqus_07.png)

   ```html
   <div id="disqus_thread"></div>
   <script>
   
   /**
   *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
   *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
   /*
   var disqus_config = function () {
   this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
   this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
   };
   */
   (function() { // DON'T EDIT BELOW THIS LINE
   var d = document, s = d.createElement('script');
   s.src = 'https://EXAMPLE.disqus.com/embed.js';
   s.setAttribute('data-timestamp', +new Date());
   (d.head || d.body).appendChild(s);
   })();
   </script>
   <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
                               
   ```



   코드를 보면 PAGE_URL에는 적용한 **내 블로그 url**,  PAGE_IDENTIFIER에는 개인 **shortname**을 추가해야 하는데, 직접 입력하는 방법도 있지만 config.yml에서 입력하고 데이터를 받아올 수도 있다. 먼저 해당 태그에 이런 형식으로 데이터 값을 받아오게끔 변경한다.



   ```yaml
   this.page.url = "{{site.disqus_username}}";
   this.page.identifier = "{{page.id}}";
   ```



 그리고 ```disqus_username```  으로 설정할 내 shortname을 확인하러 가보자.   shortname은 disqus에서 지정한 내 주소의 고유 이름이라고 볼 수 있는데, Disqus메인 -> Settings -> General 에서 확인 가능하다.

   ![disqus shorname 확인](./disqus_09.png)



![disqus shorname 확인](./disqus_10.png)



먼저 메인에서 내 프로필 사진 옆 admin을 누르면 내가 추가한 주소의 통계, 설정 등을 볼 수 있다. 여기서 Setting를 클릭하고 확인하고싶은 블로그 주소로 들어간다.



![disqus shorname 확인](./disqus_11.png)



![disqus shorname 확인](./disqus_12.png)

선택하고 나면 General 탭에서 내 shortname을 확인할 수 있다.  **Shortname**을 복사해서  ``` config.yml``` 파일에서 코드를 추가한다.

```
disqus_username: 내 shortname
```



## 완료

![disqus가 적용된 화면](./disqus_13.png)

입력을 완료한 뒤에 파일을 저장하고, 내 블로그에 commit한 뒤 확인하면 이렇게 블로그에 댓글 기능이 추가된 모습을 볼 수 있다! 지금 추가한 댓글 형태는 기본값이고, 커스텀도 가능하다니 시간나면 적용해보는 것도 좋겠다.





### 참고

+ [[깃허브(Github)] 20. 깃허브 블로그 만들기(4) - 댓글 - 회복맨 블로그](http://recoveryman.tistory.com/391)









