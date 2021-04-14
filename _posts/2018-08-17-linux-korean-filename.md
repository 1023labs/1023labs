---
layout: post
title:  "리눅스에서 한글 파일명 서버 이전 후, 파일을 찾을 수 없을 때"
date:   2018-08-17 21:00:00 +0900
categories: posts
tags: [tip,파일명,한글,convmv,euc-kr,find,nginx,ubuntu,utf-8]
redirect_from: /posts/44
--- 
10년이 넘은 홈페이지 자료를 마이그레이션 하던 중,
파일명이 한글인 첨부파일들을 새로운 서버로 이전하니,
nginx 에서 파일을 불러오지 못한다. (물론 find 에서도 못찾을 때가 있다)

백업은 호스팅 서버에서 ftp로 mac 에 다운 받은 후,
mac에서 ubuntu 서버로 파일을 전송했다.

처음부터 압축해서 옮겼으면 별 문제 없었을 텐데.
많지 않아보여서 파일 전체를 받았더니, 머리가 아프다.


검색을 해보니, 파일명도 character 형식을 변경하는 방법(convmv)이 있어,
적용해보니 잘 된다.
처음에도 형식은 utf-8 이었고, ls 에서 한글 파일명은 잘 표시하지만, 파일을 찾을 수 없는 경우가 있었다.
그래서 강제로 euc-kr 로 한번 변경 후, 다시 utf-8로 변경하니, 잘 연결되어 해결 ^^

{% highlight bash %}
$ ls
(한글 파일명은 제대로 나오지만 파일을 찾을 수 없음)

$ convmv -t utf-8 -f euc-kr --notest ./*
(파일명을 utf-8 에서 euc-kr로 변경)

$ ls
(한글 파일명이 깨져보임)

$ convmv -f euc-kr -t utf-8 --notest ./*
(파일명을 euc-kr 에서 utf-8로 변경)

$ ls
(한글 파일명도 잘 보임, nginx로 파일 연결 잘됨. find도 파일 잘 찾음)
{% endhighlight %}
