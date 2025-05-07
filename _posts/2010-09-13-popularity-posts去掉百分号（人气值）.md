---
title: "Popularity Contest去掉百分号（人气值）"
date: 2010-09-13
categories: 
  - "website"
tags: 
  - "wordpress"
  - "插件"
---

Popularity Contest是一个比较全能的WP插件，它能够按着周期（年、月、星期）等显示文章列表，这样我们很容易来实现“文章月度排行”和“文章年度排行“等功能。

可是美中不足的是，文章列表的文章标题前面有个碍人的%，也就是人气值，插件给的设置是去不掉的。我们只有自己手动来修改了，方法也很简单，打开popularity-contest.php，查找所有的<span>，然后把“<span>....</span>”删除掉就行了，删除时注意引号一定要配对。
