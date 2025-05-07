---
title: "新浪微博同步到Twitter之RSS法"
date: 2012-05-20
categories: 
  - "software_programming"
tags: 
  - "twitter"
  - "同步"
  - "微博"
---

以前一直在使用Follow5来[同步各个微博客](http://www.jfsay.com/archives/82.html "博客或者微博客的同步小结")，自从[Follow5倒闭](http://www.jfsay.com/archives/427.html "Goodbye, Follow5")以后，我的微博客同步就嘎然而止了，因为再找不到如此优秀的同步工具了。

闲话少说，切入正题。

**原理：新浪微博→新浪微博RSS→FeedBurner→Twitter**

我们所需要做的工作就是把上面的流程连接起来即可。

**1、新浪微博→新浪微博RSS**

由于新浪微博本身不提供RSS的输出功能，这里需要借助第三方的工具（[到谷歌去寻找](https://www.google.com.hk/search?aq=f&sugexp=chrome,mod=17&sourceid=chrome&ie=UTF-8&q=新浪微博rss)）。

**2、新浪微博RSS→FeedBurner**

得到你的新浪微博RSS地址以后，去[FeedBurner](http://feedburner.google.com/)烧制一个Feed。（方法略）

**3、 FeedBurner→Twitter**

FeedBurner本身提供把烧制的Feed同步到Twitter。在Publicize——Socialize——Add a Twitter account（在此添加Twitter账户）。

该方法是通过RSS来实现把新浪微博的信息同步到Twitter，大家都知道RSS需要时间来更新，所以此同步方法存在延迟。
