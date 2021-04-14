---
layout: post
title:  "리눅스 우분투(ubuntu) crontab 설정 간단 정리"
date:   2020-04-02 09:00:00 +0900
categories: posts
tags: [tip,리눅스,스케쥴러,우분투,재시작,크론,cron,crontab,linux,scheduler,slack,ubuntu]
redirect_from: /2020/04/ubuntu-crontab.html
--- 
1) `/etc/cron.daily (hourly / monthly / weekly)` 폴더에 스크립트 파일 추가  
- 따로 설정할 필요없이 실행(root권한)  
- 실행할 스크립트 파일 확장자를 붙이면 안됨  
- 실행시간 확인  
{% highlight bash %}
$ cat /etc/crontab
{% endhighlight %}

{% highlight bash %}
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user command
17 * * * * root    cd / && run-parts --report /etc/cron.hourly
25 6 * * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6 * * 7 root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6 1 * * root test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
{% endhighlight %}

- 실행권한 추가
{% highlight bash %}
$ sudo chmod +x file_name
{% endhighlight %}

- 서버 하드용량 Slack 보내기 샘플파일( {hook-url} 은 실제 url 로 수정 )
{% highlight bash %}
#!/bin/bash

result=`df -h`

curl \
-X POST -H 'Content-type: application/json' \
--data "{ \
\"text\":\"[hi] \n \
disk: $(echo "$result" | sed ':a;N;$!ba;s/\n/\\n/g') \n \
$(date +%Y.%m.%d-%H\:%M\:%S) \", \
\"channel\":\"#service_alarm\"}" \
"https://hooks.slack.com/services/{hook-url}"
{% endhighlight %}

- 간단하지만, 세부적인 설정(시간, 권한)이 안됨  
설정이 필요없어, 하루 1번 백업의 경우 hourly 에 넣고, 시간을 확인해서 실행  
{% highlight bash %}
#!/bin/bash

cur_hour="$(date +%H)"

if [ $cur_hour == '04' ]
then

  result=`df -h`


  curl \
  -X POST -H 'Content-type: application/json' \
  --data "{ \
  \"text\":\"[hi] \n \
disk: $(echo "$result" | sed ':a;N;$!ba;s/\n/\\n/g') \n \
$(date +%Y.%m.%d-%H\:%M\:%S) \", \
  \"channel\":\"#service_alarm\"}" \
  "https://hooks.slack.com/services/{hook-url}"

fi
{% endhighlight %}

<br />

2) crontab 설정  
- crontab 설정  
{% highlight bash %}
$ crontab -e
{% endhighlight %}
- crontab 목록  
{% highlight bash %}
$ crontab -l
{% endhighlight %}
- crontab 재시작  
{% highlight bash %}
$ sudo service cron restart
$ sudo service cron start
$ sudo service cron stop
{% endhighlight %}
- crontab 설정 예제 (분 시간 일 월 요일 명령어)  
{% highlight bash %}
31 7 * * 1-5 /home/user/crontab/daily/server_check.sh
{% endhighlight %}








