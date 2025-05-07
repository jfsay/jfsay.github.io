---
title: "教你设置robots.txt"
date: 2010-11-05
categories: 
  - "website"
tags: 
  - "robots"
---

**注意：此文中**robots.txt**设置方法已经过时，最佳设置robots.txt的方法如下：[https://www.jfsay.com/archives/2465.html](https://www.jfsay.com/archives/2465.html)**

站长一般都是尽最大可能让网站内容被搜索引擎收录。网站难免会出现重复的内容，而搜索引擎见到重复的内容就会把它给降权，这样就不利于SEO，影响网站的收录以及排名。所以我们要避免搜索引擎来爬找重复的内容。robots.txt是可以用来实现这个功能的文件。现在来简单讲解一下怎样设置它。

在设置过程中始终要记住我们的目标是：避免重复。

**1、收集网站信息**

URL或者俗称作网址以及目录，搜索引擎就是通过唯一的URL来查看它上面所附着的内容。我们就是让每一个唯一的URL上面的内容也唯一。所以首先要做的就是把整个站点的URL地址找出来，可以通过工具或者手动的点击能点击的超链接。下面以静风博客为例来说明。

我所查找到的静风博客URL地址，同类型的略去不计。

- \[首页\]http://www.jfsay.com/

- \[文章页\]http://www.jfsay.com/archives/188.html

- \[评论页\]http://www.jfsay.com/archives/178.html#comment-56

- \[分类归档页\]http://www.jfsay.com/archives/category/essay

- \[作者归档页\]http://www.jfsay.com/archives/author/hillway/

- \[标签归档页\]http://www.jfsay.com/archives/tag/php

- \[日期归档页\]http://www.jfsay.com/archives/date/2010/11

- \[登录\]http://www.jfsay.com/wp-login.php

- \[文章Trackback页\]http://www.jfsay.com/archives/100.html/trackback

- \[文章Feed页\]http://www.jfsay.com/archives/100.html/feed

- \[分页\]http://www.jfsay.com/page/2

- \[分类归档分页\]http://www.jfsay.com/archives/category/essay/page/2

- \[日期归档分页\]http://www.jfsay.com/archives/date/2010/06/page/2

- \[标签归档分页\]http://www.jfsay.com/archives/tag/php/page/2

- \[作者归档分页\]http://www.jfsay.com/archives/author/hillway/page/2

**2、设置robots.txt**

针对上面收集到的网页地址，我们来设置robots.txt文件。

User-agent: \*  #针对所有机器人

Disallow: /index.php  #不允许访问首页

Disallow: /archives/category/  #不允许访问分类归档页

Disallow: /archives/author/  #不允许访问作者归档页

Disallow: /archives/date/  #不允许访问日期归档页

Disallow: /archives/tag/  #不允许访问标签归档页

Disallow: \*/trackback  #不允许访问trackback

Disallow: \*/feed  #不允许访问feed

Disallow: \*/comments  #不允许访问评论

Disallow: /page/  #不允许访问分页

其中分类归档分页已经“#不允许访问分类归档页”，自然其下的分页也不允许访问了，所以不必重复设置。

用wordpress搭建的网站一般wp-开头的后台文件目录不允许访问，也就是：

Disallow: /wp-

以及配置文件不允许访问。

Disallow: /cgi-bin

还有一些附带参数的地址一般不允许访问。

Disallow: /\*?\*

Disallow: /\*?

Disallow: /?s=

通常需要在robots.txt中指明站点地图的路径。

Sitemap: http://www.jfsay.com/sitemap.xml

Sitemap: http://www.jfsay.com/sitemap.xml.gz

Sitemap: http://www.jfsay.com/sitemap\_baidu.xml

到这里，robots.txt文件已经设置完成了。

注意：

Disallow: / trackback / 和 Disallow: / trackback的区别

Disallow: / trackback /表示不允许访问目录名为trackback的页面

Disallow: / trackback表示不允许访问网址后面含有trackback关键字的页面

**3、检测robots.txt**

对于设置完成的robots.txt是否确实按着我们的意图运转，可以通过[谷歌网站管理员工具](https://www.google.com/webmasters/tools/)中的“抓取工具的权限”来进行测试。

对于漏网之鱼，我们时常通过site命令来查看搜索引擎的收录结果来进行填补以及微调。

我的robots.txt文件，切忌拷贝，因为每个站点的目录结构不尽相同，有些设置在不同的站点会不起作用或者起反作用。

User-agent: \*

Disallow: /cgi-bin

Disallow: /wp-

Disallow: /index.php

Disallow: /archives/category/

Disallow: /archives/author/

Disallow: /archives/date/

Disallow: /archives/tag/

Disallow: \*/trackback

Disallow: \*/feed

Disallow: \*/comments

Disallow: /page/

Disallow: /\*?\*

Disallow: /\*?

Disallow: /?s=

Sitemap: http://www.jfsay.com/sitemap.xml
