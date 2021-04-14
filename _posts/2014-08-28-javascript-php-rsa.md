---
layout: post
title:  "javascript+php, RSA 암호화"
date:   2014-08-28 21:00:02 +0900
categories: posts
tags: [tip, 개발, 암호화, 웹취약성, javascript, php, RSA]
redirect_from: /posts/21
---
웹 취약성 검사에서 javascript + php 암호화 소스를 찾던 중, AES소스를 찾아 적용해 놓았으나  
보안에 취약하여 RSA암호화로 변경해야한다는 보안팀의 권고(경고?)!!  
살짝 넘어가보려고 AES암호화를 살짝 적용해 두었더니 딱 걸렸다.&nbsp;에궁~~

그래서 다시 github를 검색.  
몇가지 소스 테스트 하면서 잘 작동하는 소스 발견...

[https://github.com/mvhaen/phpseclib-jsbn-rsa](https://github.com/mvhaen/phpseclib-jsbn-rsa)

그누보드에 적용해보니 잘 동작합니다만,  
RSA암호화 과정이 복잡하여 그런지 AES암호화 보다 시간이 많이 걸린다. 대략 3초.

일단 적용하고, 좀 더 빠르게 동작하는 소스가 있는지 찾아봐야겠다.  
다행히 웹취약성 검사는 무사 통과 ^^
