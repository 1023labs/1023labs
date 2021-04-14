---
layout: post
title:  "blogger에 구글 analytics 코드 넣는 방법"
date:   2014-09-15 21:00:01 +0900
categories: posts
tags: [tip,구글분석,블로거,템플릿,analytics,blogger,google,template]
redirect_from: /posts/33
--- 
1. google analytics 에 들어가서 속성 추가하고, 트래킹 ID를 복사


2. "blogger 설정 > 기타" 메뉴로 들어가서 제일 하단에 "google 애널리틱스" 웹속성 ID를 넣는다.  
(예, UA-000000-1)


3. 사용자정의 탬플릿을 사용하는 경우, "템플릿 > html편집"에 들어가서 </head> 테그 앞에
{% highlight html %}
<b:include data='blog' name='google-analytics'/>
{% endhighlight %}

코드를 추가한다.  
( 최근 탬플릿을 사용중이거나, 동적뷰 탬플릿을 사용중이면 건너뛰기. 위 include태그가 있는지 확인 )

