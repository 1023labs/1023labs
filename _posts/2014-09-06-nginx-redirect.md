---
layout: post
title:  "nginx 옛날 도메인, 새 도메인으로 rewrite"
date:   2014-09-06 21:00:00 +0900
categories: posts
tags: [tip,설정,domain,nginx,rewrite]
redirect_from: /posts/31
--- 
도메인 바꿀경우, nginx 설정에서 새 도메인으로 rewrite 하는 방법

1. nginx 설정파일을 수정합니다.
{% highlight bash %}
$ vi /etc/nginx/sites-enabled/domain
{% endhighlight %}

2. 다음 내용을 추가합니다.
{% highlight nginx %}
server_name old1.com old2.com old3.com new.com;

if ($host != 'new.com' ) {
  rewrite ^/(.*)$ http://new.com/$1 permanent;
}
{% endhighlight %}


3. nginx restart
{% highlight bash %}
$ sudo service nginx restart
{% endhighlight %}
파라미터도 잘 넘기네요.