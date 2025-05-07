---
title: "博客留一手，WordPress导入文章到Blogger"
date: 2014-03-12
categories: 
  - "website"
tags: 
  - "wordpress"
  - "博客"
  - "同步"
  - "备份"
---

我对网络世界的数据安全性和稳定性存怀疑态度，毕竟这些0、1数据看得见摸不着，指不定哪一天就灰飞烟灭了。

现在在写的博客的每一篇文章也是辛辛苦苦耗时耗力地一个字一个字码出来的，虽然写得不怎么样但也是心血之作，万一哪天没有了定会痛苦不已。所以在很久以前我就把[文章保存在本地](http://www.jfsay.com/archives/730.html "静风博客部分文章汇总")，可能在不久的将来会印成纸张。

以前有想过把博客的文章同步到新浪搜狐网易博客上，只是这些BSP都不支持WordPress文件导入的功能，虽然WordPress的插件大军中存在类似功能的插件，但是我用着很不舒服：影响正常发文，偶尔出错，而且占有CPU资源。我试图寻找一个通过RSS同步博客的方法，貌似人人和FaceBook提供。总觉得这些强社会关系社区和博客精神是相悖的，非要注册才能浏览，才能发言，而且把写作者绑在你的网站上。

于是我选择了Blogger作为博客的备份之选，它支持XML文件的导入导出，很是方便。如果某一天我的域名到期、服务器崩溃，在网络上至少还有一个存放梦想的地方。

WordPress导入文章到Blogger的步骤是（也就是个导出导入的过程）：

1.WordPress后台导出文章为XML文件

2\. 进行格式转换（没做这一步的话下一步没法进行，因为WordPress导出的XML文件无法直接导入Blogger。之前我使用的是在线转换服务，现在提供这种服务的的网站越来越少，还好WordPress有导出Blogger的插件，名字叫做「Export to Blogger」。）

3\. Blogger导入XML文件

以后大概每半年会把博客的文章导入到Blogger里，有兴趣可以围观[Blogger上的静风博客](https://jingfengblog.blogspot.com)吧，网址如下：https://jingfengblog.blogspot.com

PS: Blogger提供自定义HTML的功能，还可以添加AdSense，自由度比较大，但我用起来还是感觉不方便。
