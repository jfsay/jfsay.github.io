---
title: "促使WP-PostViews插件作者排除中国大陆搜索引擎机器人"
date: 2013-06-25
categories: 
  - "website"
tags: 
  - "wordpress"
  - "wp-postviews"
  - "插件"
---

在我刚开始使用WordPress经典插件WP-PostViews为博客文章计数的时候，就发现[WP-PostViews存在一个问题](http://www.jfsay.com/archives/721.html "让WP-PostViews排除（国内）机器人的访问数")，它不能排除掉中国大陆的搜索引擎机器人，也就是说文章的计数中包含了机器人（或蜘蛛）的浏览量。这样，即使你在插件的设置选项中排除了机器人的访问数，但是不久你将发现文章的Views会出现异常增长。

这个问题只对中国大陆的网站有影响，因为插件作者并没有考虑到我们的国情，他在WP-PostViews的Exclude Bot Views code中并没有排除掉baidu、360、soso、sogou的蜘蛛，而这几个正是我国广大网民使用最多的搜索引擎。

我们可以修改WP-PostViews插件的代码来排除掉国内的搜索蜘蛛，确保文章访问数的纯净。（[方法点这里](http://www.jfsay.com/archives/721.html "让WP-PostViews排除（国内）机器人的访问数")）

但是这两天WP-PostViews连升两级，我又懒得每次都自己去修改插件代码。于是抱着试一试的态度联系插件作者，让他把国内的蜘蛛加进去，这样对于我来说就一劳永逸了。

说干就干，找到Lester Chan的电子邮箱，一封求助邮件发了过去。

没想到他很快就回复了我的邮件：

> Can I know what is the useragent baidu and soso used? I can add it and commit the code. If you can paste just the difference here it would be good.

他让我把国内蜘蛛的useragent发给他，于是我就把baidu、360、sogou、sosou的useragent统统发给了他，顺便把这几个搜索引擎的市场份额也告诉了他。

没过多久，作者给我发来邮件说已经添加了代码。我上Github看到作者wp-postviews.php的备注已经注明[Add China search engines bots](https://github.com/lesterchan/wp-postviews/)了。

以前听过联系国外作者很容易也很热心，这次体会到了。
