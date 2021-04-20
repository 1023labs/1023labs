---
layout: post
title:  ".htaccess 파일로 항상 https 로 redirect 하기 "
date:   2021-04-20 11:32:21 +0900
categories: posts
tags: [tip,php,htaccess,https,ssl,redirect,codeigniter]
--- 
.htaccess 파일에서 항상 https 로 redirect 하기 

<br />

아래 내용을 기존 파일에 추가

{% highlight php %}
RewriteEngine on
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ https://www.domain.com/$1 [R,L]
{% endhighlight %}

<br />

CodeIgnigter 사용하는 경우
{% highlight php %}
SetEnv CI_ENV production

RewriteEngine on
RewriteCond %{SERVER_PORT} 80
RewriteRule ^(.*)$ https://www.domain.com/$1 [R,L]

RewriteCond %{REQUEST_URI} !^(/index\.php|/assets/|/robots\.txt|/favicon\.ico)
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?$1 [L]
{% endhighlight %}

<br />

