---
layout: post
title:  "git 이용한 wordpress 배포"
date:   2014-08-28 21:00:04 +0900
categories: posts
tags: [tip,개발,배포,deploy,git,wordpress]
redirect_from: /posts/23
--- 
제목이 너무 거창하다. 개발 유단자는 Pass~~  
웹개발을 한지 몇년인데, 아직까지도 서버에 배포할 때는, ftp를 열어서, 수정한 파일을 기억한 후, upload를 해왔다.  
이것도 귀찮아서 최근엔, 직접 ftp로 파일열어서 서버에서 직접 수정하며 살아왔다.

그러다가, git을 사용해서 소스 버젼관리를 하고, 배포를 자동화 하고 ~  
하는 것을 아주 살짝 봤더니만, 역시 나의 지난 세월은 머리가 나빠서 몸이 고생했던 시간들이다.

검색해보니 wordpress 배포를 위한 다양한 방법들이 있다.  
역시 문제는 방법을 다 써놨는데도 눈에 안들어오고 해보기 겁도나고 귀찮기도 하고 ^^  
(시간이 흘러도 개발실력이 늘지않은 가장 큰 이유)

걍 내가 아는수준에서 편하게 해보기로 마음먹고, 잔머리를 살짝 굴려본다.ㅎㅎ  
<br/><br/>

#### [배포 시나리오]
1. 로컬에서 wordpress 수정  
2. git push  
3. 서버에 ssh접속해서 git pull  
<br/><br/>

#### [환경]  
- 로컬 : mac(apache + mysql)  
- 서버(가상서버) : ubuntu 12.04 (nginx + mysql)  
- bitbucket.com 이용  
<br/><br/>

#### [예상되는 문제]  
1. 로컬 관리자메뉴에서 설정값(DB)을 바꿀 경우, 서버(DB)에 자동으로 적용이 안됨  
2. 배포 rollback이 필요할 경우도 git 을 활용  

또 생기는 문제는 그때 해결하고. ㅋㅋ 그럼 시작 ~  
1) 로컬에서 워드프레스 설치하고, 사이트를 만들었다.  
2) 로컬DB접속용 wp-config.php수정 & wp-local-config.php 추가  

`wp-config.php` 파일 생성
{% highlight php %}
/** Local Database Setting **/
$local_config_file = dirname(__FILE__) . '/wp-local-config.php';
if (file_exists( $local_config_file )) {
  require $local_config_file;
  define('WP_DEBUG', true);
  define('WP_DEBUG_DISPLAY', true);
  define('WP_DEBUG_LOG', true);
} else {
  // ** MySQL settings - You can get this info from your web host ** //
  /** The name of the database for WordPress */
  define('DB_NAME', 'databasename');
  /** MySQL database username */
  define('DB_USER', 'databaseuser');
  /** MySQL database password */
  define('DB_PASSWORD', 'databasepassword');
  /** MySQL hostname */
  define('DB_HOST', 'localhost');
  /** Database Charset to use in creating database tables. */
  define('DB_CHARSET', 'utf8');
  /** The Database Collate type. Don't change this if in doubt. */
  define('DB_COLLATE', '');
}
{% endhighlight %}

<br/><br/>

`wp-local-config.php` 파일 생성
{% highlight php %}
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'local database name');
/** MySQL database username */
define('DB_USER', 'local database user');
/** MySQL database password */
define('DB_PASSWORD', 'local database password');
/** MySQL hostname */
define('DB_HOST', 'localhost');
/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');
/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');
{% endhighlight %}

<br/><br/>

3) bitbucket에서 repository 만들고, 소스 push  
`.gitignore` 파일생성
{% highlight code %}
wp-content/*
!wp-content/plugins/
!wp-content/themes/
wp-local-config.php

# deploy
srv-deploy/*
{% endhighlight %}

4) 서버에서 git clone 해서 소스파일 설치

5) scp이용, uploads폴더 업로드

6) 로컬DB 백업 & 서버 복원

7) 다음번 배포를 위한 bash 스크립트 작성
`./srv_deploy/deploy.sh` 파일 생성
{% highlight bash %}
#!/bin/bash
ssh user@blog.domain.com "cd ./www/test_blog/; git pull "
{% endhighlight %}

 

8) 쉘에서 배포 스크립트 실행
{% highlight bash %}
$ ./srv_deploy/deploy.sh
{% endhighlight %}

<br/><br/>

#### [결과]
- 일단 아직은 잘 된다. ㅎㅎ git push 하고, 스크립트만 실행하면, 수정한 파일 git에서 알아서 관리해주니 쫌 편하다.  
- rollback하기 좋게 소스폴더랑 업로드 폴더 구분해서, 소스폴더 전체를 clone하여 배포해보고 싶었으나, 음.... !^#%@^!@#&@^#  
- 아주 쉽고, 완벽하게 wordpress 배포를 하는 무언가가 당연히 있을 것 같다. ^^  
- 사용자가 많으면 배포과정에서 뭔가 오류가 생길 것 같은 불길한 이 느낌?  
- 영감을 주신 몇몇 개발자 분들께 속으로 감사( 본인들은 모르고 계심 )


