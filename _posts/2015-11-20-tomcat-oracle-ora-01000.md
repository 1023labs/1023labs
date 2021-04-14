---
layout: post
title:  "Tomcat 오라클에서 오류. ORA-01000: 최대 열기 커서 수를 초과했습니다"
date:   2015-11-20 21:00:00 +0900
categories: posts
tags: [tip,오라클,오류,자바,초과,최대,커서,톰캣,java,ora-01000,oracle,preparedStatement,tomcat]
redirect_from: /posts/40
--- 
[http://serendipity.tistory.com/65](http://serendipity.tistory.com/65){:target="_blank"} 를 참고했습니다.

톰캣에서 "ORA-01000: 최대 열기 커서 수를 초과했습니다" 오류가 발생하는 것은  
오라클 프로세스당 커서수가 증가되어 발생되는 에러.


1) 쿼리로 오라클 프로세스 당 커서수를 확인  
{% highlight sql %}
SELECT sid, count(sid) AS cursor
FROM V$OPEN_CURSOR
WHERE user_name = 'SCOTT'
GROUP BY sid
ORDER BY cursor DESC
{% endhighlight %}

접속자수에 따라 다르지만, 오라클 cursor 수가 100개(일반적인 사이트는 20개)가 넘는 세션에서 사용하는 SQL문장은 의심할 필요 있음.

<br />

2) SQL문에서 사용하는 커서수  
{% highlight sql %}
SELECT sql_text, count(sid) cnt
FROM V$OPEN_CURSOR
GROUP BY sql_text
ORDER BY cnt DESC
{% endhighlight %}

커서수가 많은 sql 문장을 찾아보면, 자바에서 preparedStatement가 close()되지 않았을 확률이 높음  
특히 for문이나 Loop문에서 preparedStatement를 사용하는 부분 확인 필요.



