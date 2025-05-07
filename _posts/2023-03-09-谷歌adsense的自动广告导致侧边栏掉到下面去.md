---
title: "谷歌AdSense的自动广告导致侧边栏掉到下面去"
date: 2023-03-09
categories: 
  - "website"
tags: 
  - "adsense"
  - "wordpress"
  - "侧边栏"
---

今天发现博客的网页打开很奇怪，原来是侧边栏掉到下面去了。本来左侧是文章内容，右侧是侧边栏，现在变成了左侧是文章内容，下面是谷歌AdSense广告，再下面才是侧边栏。

网站用的是谷歌AdSense的自动广告，看来是谷歌将广告插入到文章内容和侧边栏之间了。出错的网页结构如下：

```
<div class="row" style="height: auto !important;"> 
     <div id="primary" class="content-area col-lg-8" ></div>/*文章内容*/
     <div class="google-auto-placed" style="width: 100%; height: auto; clear: both; text-align: center;"></div>/*谷歌AdSense广告*/
     <aside id="secondary-1" class="sidebar sidebar-secondary-1 text-left col-lg-4" ></div>/*侧边栏*/
</div>
```

我一开始以为是谷歌自动广告的问题，登录AdSense的自动广告设置页面也找不到可以配置的选项，之后去AdSense的帮助论坛去发帖求助。

后来网上有人说AdSense的自动广告会破坏页面显示样式，因为AdSense自动广告通过分析页面的结构来插入广告，如果网页结构有问题会导致页面错乱。这时我觉得可能我的主题有问题，通过浏览器自带的开发者工具，发现class="row"用的是弹性布局display: flex，在class="row"中添加以下代码问题就解决了：

```
flex-direction: row;  /*作为一行，水平地显示弹性项目*/
flex-wrap: nowrap;    /*flex中的元素被摆放到一行*/
```

这样把文章内容和侧边栏摆到一行去了，而且不换行，谷歌的自动广告就没法在它们之间插入广告把侧边栏挤掉到下面去了。
