---
layout: post
title:  "csv파일 mysql import 하기"
date:   2014-08-29 21:00:00 +0900
categories: posts
tags: [tip,csv,import,mysql,mysqlimport]
redirect_from: /posts/29
--- 
1. 테이블을 먼저 만든다.

2.
{% highlight bash %}
$ mysqlimport -u root --local --fields-terminated-by=',' database_name table_name.csv
{% endhighlight %}