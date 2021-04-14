---
layout: post
title:  "윈도우에서 오라클 sys 암호 잊었을 때 sqlplus 로 접속하는 방법"
date:   2016-04-13 21:00:00 +0900
categories: posts
tags: [tip,암호,오라클,윈도우,oracle,sqlplus,sys,sysdba]
redirect_from: /posts/43
--- 
오라클에서 sys 암호 잊었을 때, sqlplus 이용해서 접속하는 방법
 
{% highlight bash %}
C:\> sqlplus /nolog
SQL> conn sys@orcl /as sysdba   (orcl은 접속하려는 DB)
{% endhighlight %}

하고 아무 암호나 입력하니 로그인이 된다.


