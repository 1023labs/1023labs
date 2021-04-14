---
layout: post
title:  "gmail smtp를 이용한 메일 보낼 때, 보낸 메일주소 변경하려면"
date:   2014-08-28 21:00:06 +0900
categories: posts
tags: [tip,메일주소 수정,변경,보낸사람,from,gmail,mail,send,sendmail]
redirect_from: /posts/26
--- 
gmail smtp를 이용해서 메일 보내기를 구축해 놓았더니,  
대표메일이 아니고 세팅한 gmail계정으로 보낸사람이 표시됩니다.  
소스코드에서 from 메일주소를 세팅해줘도 바뀌지 않네요.  

그럴때, 지메일 [환경설정] > [계정 및 가져오기] > [다른 주소에서 메일 보내기] 를 설정해주니 가능하네요.  
다른 이메일 주소를 추가하고, 기본 주소로 변경하고, "별칭으로 처리" 항목은 체크를 해제했습니다.