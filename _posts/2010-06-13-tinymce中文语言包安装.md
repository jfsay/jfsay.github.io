---
title: "TinyMCE中文语言包安装"
date: 2010-06-13
categories: 
  - "website"
tags: 
  - "tinymce"
---

到官方网站下载中文包tinymce\_lang\_pack.zip，将其解压后放到TinyMCE文件夹的如下目录jscripts\\tiny\_mce中，覆盖里面的文件，然后到页面的tinyMCE初始化语句 tinyMCE.init 中加上一行：

language : ”zh”,

注意不要丢失最后的逗号“,” ，不然会出错。
