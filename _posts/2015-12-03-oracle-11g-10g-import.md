---
layout: post
title:  "오라클 11g에서 export 한 파일이 10g에 import 되지 않을때"
date:   2015-12-03 21:00:00 +0900
categories: posts
tags: [tip,10g,11g,백업,복원,에러,엑스포트,임포트,client,exp,export,imp,IMP-00000,IMP-00010,import,oracle]
redirect_from: /posts/42
--- 
서버는 오라클 최신버전을 구매해서 11g를 설치했다.  
운영중 서버에서 export한 dmp 파일을 개발서버에 import하려고 하니

{% highlight bash %}
IMP-00010: 엑스포트 파일이 유효하지 않고, 헤더가 검증에 실패했습니다
IMP-00000: 임포트가 실패로 끝났습니다
{% endhighlight %}


에러가 나면서 dmp 파일이 열리지 않는다.

11g에서 덤프받은 파일을 10g에 올리려고 해서 발생하는 에러라고 함.

해결방법은 여러가지가 있는 듯 하다.

- 11g 에서 version=10.2 옵션을 붙여서 export 다시 받기  
- client 10g 버전으로 11g에 접속해서 export 받기  
- client 11g 에서 10g로 imp 하기  


DB서버에 외부접속이 차단된 관계로, 다시 export를 받을 수 없었다.  
3번째 방법 "client 11g에서 10g로 imp 하기"로 결정.  
오라클 클라이언트 다운받고 설치하고, TNS등록해주고 하는 시간이 오래 걸리긴 했으나,

다행히 imp는 오류 없이 성공!