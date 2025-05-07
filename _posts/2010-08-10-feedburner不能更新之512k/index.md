---
title: "Feedburner不能更新之512K"
date: 2010-08-10
categories: 
  - "website"
tags: 
  - "feedburner"
---

自从使用Feedburner之后一直感觉很好，它既能绑定自己的域名，又可以添加国产的订阅器，新发表的文章一般在半个小时内会投递到订阅器中，关键是有谷歌的技术支持。

前两天突然出问题了，好几天的文章都没有更新。登录Feedburner选择Optimize查看Your Feed和XML source都是不可用，然后选择Troubleshootize点击其中的Resync Now出现了两条错误：

1. There is an issue that must be addressed with your source feed for the feed "静风博客"
2. Your feed filesize is larger than 512K. You need to reduce its size in order for FeedBurner to process it. Tips for controlling feed file size with Blogger can be found in Tech Tips on FeedBurner Forums, our support site.

上网寻找原因发现FeedBurner will not process an original feed from your blog if it is greater than 512K in size.就是说原始Feed源不能超过512K，超过了FeedBurner就会罢工了。于是赶紧找出来Rss输出文件，把查询语句select \* from comment order by time desc改成select \* from comment order by time desc limit 10

然后Resync Now显示成功，再pinging FeedBurner，查看Google Reader发现很快就有新条目了。
