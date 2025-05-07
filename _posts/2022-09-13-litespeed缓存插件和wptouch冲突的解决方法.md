---
title: "LiteSpeed缓存插件和WPtouch冲突的解决方法"
date: 2022-09-13
categories: 
  - "website"
tags: 
  - "博客"
  - "缓存"
---

由于我使用的虚拟主机用的是LiteSpeed Web Server服务器，主机商建议安装LiteSpeed Cache缓存插件，这样可以加快WordPress网站的访问速度。一直以来我对网站的访问速度要求不高，只要网页能正常打开就行了，既然主机商这么提醒，那就试一下吧。安装LiteSpeed Cache后能明显感觉到网页加载速度加快了，以前大概等1-2秒才打开，现在瞬间就打开了。

但是发现手机端打开页面会显示桌面版的网页，而不是移动端的网页。因为我的博客一直使用WPtouch插件实现移动端的主题，相当于桌面端和移动端用的是两套主题。

最后通过bing国际版，找到WPtouch官网的帮助页面找到了解决方法。如果Google存在的话，也不至于让我在百度里找这么久找不到答案。

https://support.wptouch.com/article/1446-configuring-cache-plugins-for-wptouch

官方《Configuring cache plugins for WPtouch》给出的解决方法如下：

LiteSpeed Cache

When using the LiteSpeed Cache on your WPtouch-powered website, configuring it to play nicely with WPtouch is very easy. Please follow the steps below.

1. Go to the LiteSpeed Cache plugin's settings page
2. Click on the "Cache" tab
3. Enable the "Cache Mobile" settings
4. Purge LiteSpeed Cache's cache

简单来说就是打开「缓存手机访客」的按钮，我一开始以为这个功能OFF才是手机端不应用桌面版的缓存，原来是打开这个功能选项才是。这个选项的备注是：Serve a separate cache copy for mobile visitors. 意思是为移动端设置专门的缓存。

步骤如下：

1. 在「LiteSpeed缓存设置」下的「缓存插件」下的「缓存手机访客」按钮打开。
2. 在「移动用户代理列表」中添加以下内容:

iPhone  
iPod  
Android  
BB10  
BlackBerry  
webOS  
IEMobile/7.0  
IEMobile/9.0  
IEMobile/10.0  
MSIE 10.0  
iPad  
PlayBook  
Xoom  
P160U  
SCH-I800  
Nexus 7  
Touch
