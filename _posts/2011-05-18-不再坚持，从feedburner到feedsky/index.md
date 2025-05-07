---
title: "不再坚持，从Feedburner到Feedsky"
date: 2011-05-18
categories: 
  - "website"
tags: 
  - "feedburner"
  - "feedsky"
---

博客创建伊始就使用Feedburner来烧制网站的RSS，Feedburner没有中文界面，帮助文档也很稀缺，连关键的域名绑定也被墙得严严实实，完全靠自己的摸索才勉强搞懂怎么使用Feedburner，当时可没少费工夫。为的只是使用谷歌的服务，用着放心。

一直以来使用Feedburner也很融洽，不仅更新迅速，而且提供同步到twitter的功能。问题就是它的域名绑定被墙了，可替换的IP也消耗殆尽，在国内使用起来已是相当地麻烦。再者，对于国内读者使用国产的RSS订阅器（比如：鲜果、有道、抓虾等），会出现文章得不到更新的问题。

于是，开始使用Feedsky了。可能吧介绍了如何在Feedburner和Feedsky中平滑地更换博客RSS Feed地址。简单地说就是：

1. 在Feedburner上烧制的Feed地址是：feeds.feedburner.com/jingfengblog，绑定域名之后，只能使用二级子目录作为feed地址是：feed.jingfeng.info/jingfengblog
2. 在Feedsky上烧制的Feed地址是：feed.feedsky.com/jingfengblog，绑定域名之后，可以使用的feed地址是：feed.jingfeng.info，也可以使用二级子目录作为feed地址是：feed.jingfeng.info/jingfengblog

从上面可以看出，使用Feedburner和Feedsky可以得到相同的feed地址是：feed.jingfeng.info/jingfengblog，但是前提是feeds.feedburner.com/jingfengblog和feed.feedsky.com/jingfengblog当中的名称jingfengblog必须相同，没有被别人使用。推荐网站的feed地址采用二级子目录的形式，这样有利于在Feedburner和Feedsky中平滑切换Feed地址。

静风博客的Feed地址是：feed.jingfeng.info/jingfengblog
