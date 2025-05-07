---
title: "LiteSpeed缓存插件首页显示的问题（失效）"
date: 2022-09-16
categories: 
  - "website"
tags: 
  - "litespeed"
  - "博客"
---

这几天都在折腾LiteSpeed Catch这个插件，主要的问题就出在手机端和桌面端（PC）的显示上。在《LiteSpeed缓存插件和WPtouch冲突的解决方法》已经解决了手机端和桌面端（PC）分别显示两个主题版本的问题，但是又出现了首页显示的新问题：手机端显示桌面端的首页版式。

我找了LiteSpeed Catch和Wptouch的帮助文档都没有解决问题，去bing找了LiteSpeed Catch homepage关键字的英文网页，也没有找到解决办法。

我在LiteSpeed缓存插件的「例外规则」里的「不缓存的URL」中添加了首页的完整域名和index.php的记录，还是没有解决。

昨天突然看到了LiteSpeed Catch文档中对「Guest Mode」的介绍，我尝试着把这个开关打开，没想到首页显示异常的问题解决了，现在手机端和桌面端（PC）分别显示不同的页面版式了。「Guest Mode」的说明如下：

> Guest Mode
> 
> OFF
> 
> When Guest Mode is enabled, LSCache serves a default version of the page from cache for a visitor's first request. This means, for this first visit only, ESI is not enabled, and no cache varies are considered.
> 
> Once the HTML of the page is loaded, then an Ajax call is used to load the "correct" version of the page for that visitor (i.e., the one where ESI and cache varies are considered, and whatever optimizations you normally run on your site are used).

这段话的意思是说访客模式下，第一次加载页面调用缓存中的版本（数据可能不正确），然后再去加载「正确的数据」。说实话，读完了我也不懂这个功能是什么意思，反正问题解决了。

update 9月24日

最终还是没有解决这个问题，首页还是随机的显示桌面版和移动版，我被迫[换了自适应的主题](https://www.jfsay.com/archives/2072.html)，停用了WPtouch插件
