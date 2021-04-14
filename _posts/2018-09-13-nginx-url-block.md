---
layout: post
title:  "NGINX 특정 URL BLOCK 설정"
date:   2018-09-13 21:00:00 +0900
categories: posts
tags: [tip,로그,매칭,설정,정규식,해킹,block,config,log,nginx,request]
redirect_from: /posts/47
--- 
10년도 전에 오픈소스 게시판을 이용해 만들었던 홈페이지를 새롭게 리뉴얼하니,  
예전 URL로 요청이 많아서, 로그가 너무 많이 쌓였다.

nginx 로그를 열어보니, *.php 형태로 들어오는 request가 너무 많아서 로그가 너무 빨리 쌓였고,  
별건 아니더라도 서버에 부담도 있었을 것이다.

아마도 오픈소스 게시판을 이용한 홈페이지가 해킹에 이용됐던 것 같다.


검색해보니, nginx 설정에서 정규식 매칭을 통해 처리가 가능하다.  

`/etc/nginx/sites-avaliable/(서비스).conf` 파일 내에 server 항목 안에, 아래 설정을 추가하고,

{% highlight nginx %}
location ~ \.php($|/) {
  deny all;
}
{% endhighlight %}
브라우저에서 php로 끝나는 url을 호출하니,



확인해보니, 어플리케이션 로그도 많이 줄었다.



{% highlight bash %}
{% endhighlight %}
