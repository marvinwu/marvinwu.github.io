---
layout: post
title: How to Host a site 
---



[hosting on github & dropbox ??](http://alexcican.com/post/guide-hosting-website-dropbox-github/)


https://github.com/jekyll/jekyll


#### what is the difference between user and proejcdt site ?


mainly project site you need to host at sub directory


#### how to setup jkyLL ?

* create a github page 
* clone to your local,
* inside your local directory,

use the [official image](https://github.com/jekyll/docker):

docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll \
  -it -p 4000:4000 jekyll/jekyll jekyll s


  http://ip:4000

  #### how to change JKYLL themes ?

  
#### how to use wordpress github sync ?

* [create a personal token](https://github.com/settings/tokens/new)

![a snap shot here](https://dl.dropboxusercontent.com/spa/8a95omz6xkznrmw/yilzu89t.png)

* copy the token and fill in wordpress admin-> setting-> wordpress <--> github sync oauth token 

* copy the web hook address and fill in git hub repo-> setting webhook & services -> webhook address

* geneerate web secrets 

* install wp markdown
* 
