---
layout: post
title:  "맥에서 터미널 프롬프트에 git branch 추가하기"
date:   2015-02-04 21:00:00 +0900
categories: posts
tags: [tip,맥,브랜치,터미널,프롬프트,bash_profile,branch,git,mac,osx,prompt,terminal]
redirect_from: /posts/38
--- 
master에서만 살 때는 몰랐는데, branch를 만들기 시작하니  
확인하려는 마음에 "git b / git branch" 를 계속 입력하게 되는군요.

가끔 치려고 검색해서  

[http://martinfitzpatrick.name/article/add-git-branch-name-to-terminal-prompt-mac/](http://martinfitzpatrick.name/article/add-git-branch-name-to-terminal-prompt-mac/){:target="_blank"}  
을 따라했습니다.

 


1) `.bash_profile` 열기
{% highlight bash %}
$ vi ~/.hash_profile
{% endhighlight %}

<br />

2) 아래 내용 추가
{% highlight bash %}
# Git branch in prompt.

parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
{% endhighlight %}

<br />

3) 적용
{% highlight bash %}
$ source ~/.bash_profile
{% endhighlight %}
잘 되내요~