---
title: "Feed文章后面出现不能显示的图片"
date: 2010-09-15
categories: 
  - "website"
tags: 
  - "wordpress"
  - "插件"
---

在Google Reader中查看自己的博客，发现每篇文章后面出现一个不能显示图片的图标，复制图片的地址http://www.jfsay.com/?ak\_action=api\_record\_view&id=12&type=feed，然后把ak\_action=api\_record\_view&id=在Google搜索了一下，发现是Popularity Contest插件里面的语句。

问题找到源头了。打开Popularity Contest中的popularity-contest.php，注释掉ak\_action=api\_record\_view id=所在的else if语句即可。
