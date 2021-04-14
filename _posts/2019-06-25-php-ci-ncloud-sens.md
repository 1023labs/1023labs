---
layout: post
title:  "PHP codeigniter에서 ncloud SENS API 로 SMS 보내기"
date:   2019-06-25 21:00:00 +0900
categories: posts
tags: [tip,네이버,문자,문자발송,클라우드,api,codeigniter,naver,ncloud,php,SENS,SMS]
redirect_from: /posts/48
--- 
웹호스팅 이용해서 간단한 홈페이지 만들기엔 역시 php가 편하네요.
간단한 페이지 만들 때는 아직 codeigniter 3.x 버전을 사용합니다.

홈페이지에서 새 글이 올라오면 문자를 보내달라는 고객 요청이 있어서,
rest API 형태로 SMS 를 보낼 수 있는 서비스를 검색한후,
네이버 ncloud 의 SENS API 를 사용하기로 결정

API문서는 잘 되어 있는데, PHP 예제를 찾기가 어려워,
약간의 삽질을 통해 만든 PHP 샘플 공유합니다.

{% highlight php %}
// sms 보내기 추가 
$sID = "ncp:sms:kr:xxxxxxxxxxxx:project_name"; // 서비스 ID
$smsURL = "https://sens.apigw.ntruss.com/sms/v2/services/".$sID."/messages";
$smsUri = "/sms/v2/services/".$sID."/messages";
$sKey = "{서비스 ID Secret Key}";

$accKeyId = "{인증키 key id}";
$accSecKey = "{인증키 secret key}";

$sTime = floor(microtime(true) * 1000);

// The data to send to the API
$postData = array(
    'type' => 'SMS',
    'countryCode' => '82',
    'from' => '01012341234', // 발신번호 (등록되어있어야함)
    'contentType' => 'COMM',
    'content' => "메세지 내용",
    'messages' => array(array('content' => "메세지 내용", 'to' => '01056785678'))
);

$postFields = json_encode($postData) ;

$hashString = "POST {$smsUri}\n{$sTime}\n{$accKeyId}";
$dHash = base64_encode( hash_hmac('sha256', $hashString, $accSecKey, true) );

$header = array(
        // "accept: application/json",
        'Content-Type: application/json; charset=utf-8',
        'x-ncp-apigw-timestamp: '.$sTime,
        "x-ncp-iam-access-key: ".$accKeyId,
        "x-ncp-apigw-signature-v2: ".$dHash
    );

// Setup cURL
$ch = curl_init($smsURL);
curl_setopt_array($ch, array(
    CURLOPT_POST => TRUE,
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_HTTPHEADER => $header,
    CURLOPT_POSTFIELDS => $postFields
));

$response = curl_exec($ch);
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