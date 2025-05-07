---
title: "WordPress下解决百度不支持索引型sitemap的办法"
date: 2022-07-13
categories: 
  - "website"
tags: 
  - "wordpress"
---

最近在百度里发现博客里的最新文章都没有收录，登录百度搜索资源平台（站长平台）发现之前提交的sitemap的状态显示「索引型不予处理」。搜了下什么是「索引型sitemap」，得到结果是xml下不能嵌套xml，也就是说sitemap文件里显示的是最终的网址，而不能是子xml。

我的博客的sitemap是用Google XML Sitemaps插件生成的，百度之前也能用。我打开发现这个xml下还有子xml，也就是百度说的「索引型sitemap」。再搜索发现wordpress已经自带生成sitemap文件的功能了，于是停了Google XML Sitemaps插件，再访问https://www.jfsay.com/wp-sitemap.xml就是wordpress生成的sitemap了。但是等等，为什么也是xml，不是文章网址呢。如下所示：

https://www.jfsay.com/wp-sitemap-posts-post-1.xml  
https://www.jfsay.com/wp-sitemap-posts-page-1.xml  
https://www.jfsay.com/wp-sitemap-taxonomies-category-1.xml  
https://www.jfsay.com/wp-sitemap-taxonomies-post\_tag-1.xml  
https://www.jfsay.com/wp-sitemap-users-1.xml

但是，上面这些网址是固定的，分别是文章、页面、分类、标签和用户，点进去就是真正的网址了，分别把他们提交给百度就行了。不错，又省了一个插件。
