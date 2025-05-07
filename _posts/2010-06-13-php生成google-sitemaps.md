---
title: "PHP生成Google Sitemaps"
date: 2010-06-13
categories: 
  - "website"
tags: 
  - "php"
---

Google Sitemaps是在网站根目录下，建立的网站网页的xml索引文件，然后通过Google Sitemaps的提交页面，提交该xml文件，这样的话Google可以方便地找到你网站的网页索引。传统方式是Google爬虫来查找你的网页，而现在是你主动地提交自己的网页索引。显而易见的好处是，你的网站可以更好更快地被搜索引擎索引到更多的网页。

我们可以通过一些方式来生成这个sitemap，然后拷贝到网站根目录并提交，wordpress也可以通过添加插件来自动生成并主动提交。对于PHP，我们同样可以像生成RSS的XML文件一样来生成sitemap的XML文件。

提供一个PHP生成sitemap的类（google\_sitemap.class.php）和实例（google\_sitemap-example.php）文件，点击[下载地址](https://docs.google.com/leaf?id=0BylPy_4csyrXYWE2N2RmNGUtZjRlYS00OTk1LWE3MDMtMTUyMmUyYjRiN2Vk&sort=name&layout=list&num=50)。
