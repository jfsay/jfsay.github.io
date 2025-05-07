---
title: "WPtouch禁止百度转码的方法"
date: 2015-10-12
categories: 
  - "website"
tags: 
  - "wptouch"
  - "百度"
---

如果你的网站没有移动版的网站的话，百度会殷勤地不由分说地强制地给你的网页进行转码，美其名曰“便于在移动设备上浏览”。有些时候我们并不需要百度的“无故献殷勤”，不希望网页被转码。百度也给了解决方案，就是在页面的<head></head>之间加上如下的声明：

```
<meta http-equiv="Cache-Control" content="no-transform" />
<meta http-equiv="Cache-Control" content="no-siteapp" />
```

我的博客采用的是固定宽度的主题，为了便于移动设备浏览，使用了WPtouch插件。[WPtouch](http://www.jfsay.com/archives/867.html)能够自动识别移动设备，调用插件自带的移动版主题，实现页面的自适应大小——也就是说安装了WPtouch之后你不必考虑细节就拥有了一套手机版的网站了。

我是不希望被百度转码的，于是在博客的主题代码中加入了上面的那段声明，但是偶尔用手机百度搜索博客文章时，发现页面仍然被百度转码。难道百度如此狡诈，对自己制定的规则视而不见？后来我发现是我冤枉了百度，一直以来我以为我的博客只有一个主题Themes，忽略了WPtouch插件自带的主题。我只是在PC版的主题上添加了禁止百度转码的声明，没有在WPtouch的主题中添加，导致百度依然对我的博客文章进行转码。

之后通过在WPtouch的主题中添加禁止百度转码的声明后，百度已经停止了对博客文章进行转码了。

WPtouch的主题中添加禁止百度转码的声明的方法是，进入WPtouch插件的主题目录：

/wp-content/plugins/wptouch/themes/foundation/default/

在header.php文件中添加如上的声明。
