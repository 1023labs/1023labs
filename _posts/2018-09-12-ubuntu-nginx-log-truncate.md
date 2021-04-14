---
layout: post
title:  "Ubuntu Nginx 로그파일 내용 비우기"
date:   2018-09-12 21:00:00 +0900
categories: posts
tags: [tip,비우기,삭제,log,nginx,truncate,ubuntu]
redirect_from: /posts/46
--- 
nginx 로 웹서버를 오래 운영하니, 로그파일이 커져서 열기가 힘들다.

logrotate 를 설정하는게 답이겠지만,

쉽게 로그파일 내용을 삭제하려 했더니, 서비스 중에 권한 문제로 파일 삭제가 안된다.

nginx 중단하면 쉽겠지만, 중단없이 하기 위해 검색 후, 테스트해보니

truncate 명령으로 잘 된다.


[우선 로그 파일용량 확인]
{% highlight bash %}
$ du -sh *
{% endhighlight %}

<br />

s[필요할 경우, 로그 백업]
{% highlight bash %}
$ cp nginx.access.log nginx.access_bak.log
{% endhighlight %}

<br />

[로그파일 비우기]
{% highlight bash %}
$ truncate -s 0 nginx.access.log
{% endhighlight %}

