---
layout: post
title: JekyLL 
---


## Probably I should do this ?

[hosting on github & dropbox ??](http://alexcican.com/post/guide-hosting-website-dropbox-github/)



## what is the difference between user and proeject site ?


mainly project site you need to host at sub directory


## how to setup jekyLL locally ??

* create a github page 
* clone to your local,
* inside your local directory,

use the [jekyll docker official image](https://github.com/jekyll/docker):

~~~
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll \
  -it -p 4000:4000 jekyll/jekyll jekyll s
~~~

  http://yourip:4000

## how to change JKYLL themes ?

  

