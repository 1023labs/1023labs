---
layout: post
title:  "mysql에서 csv파일로 export 하기"
date:   2014-09-15 21:00:00 +0900
categories: posts
tags: [tip,csv,export,mysql]
redirect_from: /posts/32
--- 
몇가지 방법이 있는 것 같은데,  
제가 자주 쓰는 방법은

{% highlight sql %}
select col1, col2, col3, col4 from tablename
into outfile '~/filename.csv'
fields terminated by ','
enclosed by '"'
lines terminated by '\n';
{% endhighlight %}