---
layout: post
title:  "[ruby] osx에서 mariaDB 설치 후, gem install mysql2 에러"
date:   2020-09-04 20:53:21 +0900
categories: posts
tags: [tip,ruby,bundle,gem,install,mysql2,mariadb,osx,맥,error,오류,루비]
redirect_from: /posts/75
--- 
맥 osx에서 os를 새로 설치하면서, mysql이 아닌 mariaDB 를 설치했더니, 

gem install mysql2 과정에서 아래 에러가 발생



{% highlight text %}
-----
Don't know how to set rpath on your system, if MySQL libraries are not in path mysql2 may not load
-----
-----
Setting libpath to /usr/local/Cellar/mariadb/10.5.5/lib
-----
creating Makefile
{% endhighlight %}

<br />

mysql path 가 없어서 설치가 안된다고. 

bundle 할때 설치 경로를 지정해 주기 위해

{% highlight bash %}
$ bundle config build.mysql2 --with-mysql-config=/usr/local/Cellar/mariadb/10.5.5/bin/mysql_config
$ bundle 
{% endhighlight %}

성공 ^^