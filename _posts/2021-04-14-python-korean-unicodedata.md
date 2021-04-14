---
layout: post
title:  "[python] 크롤링 텍스트 한글 자음 모음 분리 문제"
date:   2021-04-14 20:39:21 +0900
categories: posts
tags: [tip,python,파이썬,한글,자음,모음,분리,NFC,NFD,unicodedata]
--- 
웹에서 크롤링 한 데이터를 python으로 처리하던 중,  

![한글 자음 모음 분리](/assets/img/python-unicodedata/img_1.png)

한글이 자음, 모음으로 분리된 텍스트 발견  
맥에서 한글명 파일 만들어서 윈도우로 보낼때 파일명이 이렇게 깨지던걸 본 기억이 있다.

크롤링 한 데이터가 아이폰에서 입력한 텍스트라 그런지 궁금하긴 하지만,  
맥에서 유니코드를 처리하는 방법이 달라서 생기는 현상으로,  
NFD(Normalization Form Decomposition) 라는 방식으로 처리하기 때문  

NFD의 경우,
{% highlight python %}
text = "어려운"
print(text[0])
ㅇ
{% endhighlight %}

NFC의 경우,
{% highlight python %}
text = "어려운"
print(text[0])
어
{% endhighlight %}

<br />

형태소 분석을 돌리는데, 특정 단어들이 추출되지 않아서 원인을 찾느라 삽질을 했다.  
jupyter notebook 에선 텍스트가 분리된 형태가 아닌 합쳐진 형태로 출력되서 원인을 찾기가 더 어려웠다.  
해결 방법은, 처리하기 전에 NFC(Normalization Form Composition) 형태로 바꿔주면 된다.

{% highlight python %}
import unicodedata

text = "어려운"
text = unicodedata.normalize('NFC', text)
print(text[0])
어
{% endhighlight %}

<br />

NFD와 NFC형식이 섞여 있는 경우에도 잘 동작한다.
