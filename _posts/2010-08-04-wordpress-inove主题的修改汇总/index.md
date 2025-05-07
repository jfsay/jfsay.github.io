---
title: "WordPress iNove主题的修改汇总"
date: 2010-08-04
categories: 
  - "website"
tags: 
  - "inove"
  - "wordpress"
---

Wordpress搭建的博客建起来第一件事就是更改主题（Themes），总觉得老外欣赏美的眼光与国人不同，他们做出来的主题虽然也美丽大方，可感觉缺少东方人简约含蓄的味道来，换了[不知多少](https://www.jfsay.com/archives/33.html "Hillway，你什么时候去操场裸跑？")主题后，终于选用了MG12的Inove主题。

在Inove主题上做了不少的修改，现总结如下。

**404页面模板（404.php）**

1、  去掉了咸湿佬图片的链接。

2、  添加了谷歌[自定义404错误页面](https://www.jfsay.com/archives/66.html)。

**主题支持函数 (functions.php)**

Wordpress默认的标签云略显单调，为此实现了彩色标签云。参考wordpress免插件实现彩色标签云

**Tags页面模板（tag-page.php）**

实现了标签云页面，由于已经添加了彩色标签云函数，故而这里的标签云页面为彩色标签云页面。参考inove主题添加标签页

**cse页面模板（cse.php）**

实现页内的谷歌搜索，也就是对搜索结果提供内页处理， 搜索后不会转跳到 Google.com.参考整合 Google 自定义搜索 CSE和美化iNove的Google自定义搜索

**底部 (footer.php)**

主要是修改了底部的CSS样式，添加了协议声明。

**文章页面模板 (single.php)**

主要在文章末尾[添加版权申明](https://www.jfsay.com/archives/204.html "文章添加链接与版权的非插件实现")以及少许广告片段。

**样式表 (style.css)**

大部分修改花在样式表上。

[导航栏和侧边栏样式的修改](https://www.jfsay.com/archives/574.html)、[侧边栏宽度的修改](http://www.jfsay.com/archives/539.html)

[延迟加载图片的实现](https://www.jfsay.com/archives/52.html "延迟加载图片的实现")、鼠标悬浮显示评论、[添加站点统计功能](https://www.jfsay.com/archives/279.html "WordPress添加站点统计功能") 、[顶部图片汇总](https://www.jfsay.com/archives/477.html)
