---
layout: post
title:  "next scripts plugin - Error: No CURL Found"
date:   2014-08-28 21:00:05 +0900
categories: posts
tags: [tip,curl,error,install,next scripts,not found,php5-curl]
redirect_from: /posts/25
--- 
ubuntu, nginx + php-fpm 환경에서 wordpress를 운영중에,  
트위터에 글 자동 발행해보려 next scripts 플러그인을 설치하니, 에러 발생.  
Error: No CURL Found ... 어쩌구 저쩌구  

php5-curl 을 설치해줬더니 잘 된다.  

{% highlight bash %}
$ sudo apt-get install php5-curl
$ sudo service nginx restart
$ sudo service php5-fpm restart
{% endhighlight %}
그럼 트위터로 자동발행이 되는지 테스트를 겸하여 ㅋㅋ