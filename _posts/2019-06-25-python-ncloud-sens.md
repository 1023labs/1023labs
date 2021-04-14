---
layout: post
title:  "python에서 ncloud SENS API 로 SMS 보내기"
date:   2019-06-26 21:00:00 +0900
categories: posts
tags: [tip,네이버,문자,문자발송,클라우드,api,hash,naver,ncloud,python,SENS,SMS]
redirect_from: /posts/49
--- 
php로 하고나니, 여기 저기서 SMS 를 보내달라는 요청이 있어서,

걍 python 으로 만들어서 google cloud function에 올려놓고 보내기로.

SMS 가 건당 비용이 발생해서 그런지, header와 hash 만드는게 살짝 복잡하여,
또 약간 삽질 해서 만든 python 샘플 입니다.

필요하신 분 참고하세요.

{% highlight python %}
import hmac, hashlib, base64
import time, requests, json
sid = "ncp:sms:kr:xxxxxxxxxxxx:project_name"

sms_uri = "/sms/v2/services/{}/messages".format(sid)
sms_url = "https://sens.apigw.ntruss.com{}".format(sms_uri)
sec_key = "{서비스 ID Secret Key}"
    
acc_key_id  = "{인증키 key id}"
acc_sec_key = b'{인증키 secret key}'
    
stime = int(float(time.time()) * 1000)
    
hash_str = "POST {}\n{}\n{}".format(sms_uri, stime, acc_key_id)
    
digest = hmac.new(acc_sec_key, msg=hash_str.encode('utf-8'), digestmod=hashlib.sha256).digest()
d_hash = base64.b64encode(digest).decode()

from_no = "01012341234"
to_no   = "01056785678"
message = "메세지 테스트"

msg_data = {
    'type': 'SMS',
    'countryCode': '82',
    'from': "{}".format(from_no),
    'contentType': 'COMM',
    'content': "{}".format(message),
    'messages': [{'to': "{}".format(to_no)}]
}
    
response = requests.post(
    sms_url, data=json.dumps(msg_data),
    headers={"Content-Type": "application/json; charset=utf-8",
            "x-ncp-apigw-timestamp": str(stime),
            "x-ncp-iam-access-key": acc_key_id,
            "x-ncp-apigw-signature-v2": d_hash
            }
)


print(response.text)
{% endhighlight %}

<br />

- key 의 종류 확인. 서비스 ID & 인증키  
- 웹호스팅의 보안 설정 문제로 curl 을 사용

1) ncloud SENS 에서 프로젝트 생성 후, 서비스 ID, secret key 복사
![ncloud SENS console](/assets/img/ncloud-sens-php/content_php1.png)

![ncloud SENS console](/assets/img/ncloud-sens-php/content_php2.png)

<br />

2) ncloud 마이페이지 > 인증키 관리 에서 인증키 생성 후, 인증키 key id, secret key 복사
![ncloud SENS console](/assets/img/ncloud-sens-php/content_php3.png)

<br />

3) ncloud SENS > SMS > Calling Number 에서 발신번호 등록
![ncloud SENS console](/assets/img/ncloud-sens-php/content_php4.png)

<br />

4) 문자발송 TEST

위 코드 참고하여 발송 테스트