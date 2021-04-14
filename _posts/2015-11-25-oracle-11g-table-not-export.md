---
layout: post
title:  "오라클(oracle) 11g 에서 사용하지 않은 테이블이 exp 되지 않을 때"
date:   2015-11-25 21:00:00 +0900
categories: posts
tags: [tip,11g,백업,복원,빈테이블,오라클,allocate,alter,empty,exp,export,extent,oracle]
redirect_from: /posts/41
--- 
오라클 백업 및 복원시 exp / imp 명령을 사용해서 복원했는데, 테이블의 개수가 다른 경우가 있다.  
11g 부터 생성하고 한번도 사용하지 않은 테이블의 경우 dmp에서 제외된다고 한다.

이럴때 강제로 테이블에 segment를 할당하기 위해,
{% highlight sql %}
ALTER TABLE  ALLOCATE EXTENT;
{% endhighlight %}
쿼리를 활용하면 됨.

<br />

빈 테이블만 ALTER 쿼리를 만들기 위해,
{% highlight sql %}
SELECT 'ALTER TABLE '||table_name||' ALLOCATE EXTENT;' FROM user_tables WHERE segment_created = 'NO';
{% endhighlight %}
를 실행하고, 쿼리 결과를 다시 실행한 다음 exp를 실행하면
모든 테이블을 export 받을 수 있다.


