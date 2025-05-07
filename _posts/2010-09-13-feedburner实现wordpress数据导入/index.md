---
title: "Feedburner实现WordPress数据导入"
date: 2010-09-13
categories: 
  - "website"
tags: 
  - "feedburner"
  - "wordpress"
---

自从转换了博客平台以后，由于两个平台的数据表的格式不一致，以前的数据导入到WP成为一个问题，不可能一篇篇的复制吧，这样既没有效率，又容易出错。

我于是想到到一个稍微可行的方法是利用RSS。我的RSS以前是用Feedburner烧制的，Feedburner可以查看XML Source，把这个东西复制出来保存为.xml格式的文件，然后在WP中安装RSS Importer工具，导入保存的xml文件即可。
