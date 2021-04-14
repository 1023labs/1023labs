---
layout: post
title:  "우분투(ubuntu) 타임존(time_zone) 변경"
date:   2015-03-18 21:00:00 +0900
categories: posts
tags: [tip,변경,수정,우분투,타임존,timezone,ubuntu]
redirect_from: /posts/39
--- 
해외 클라우드 서비스 이용할 경우,  
서버 세팅하고 나서, 우분투의 타임존을 확인합니다.

{% highlight bash %}
$ date
{% endhighlight %}

<br />

국내 서비스를 할 경우, 타임존을 Asia/Seoul 로 수정하려면

{% highlight bash %}
$ sudo dpkg-reconfigure tzdata
{% endhighlight %}

하고, Asia -> Seoul 순서로 선택해주면 끝.



