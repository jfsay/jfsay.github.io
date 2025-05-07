---
title: "博客的流量用完的解决过程"
date: 2021-06-29
categories: 
  - "website"
tags: 
  - "博客"
  - "流量"
---

我的博客用的是[廉价的虚拟主机](https://my.laoxuehost.com/aff.php?aff=769)空间，只有500MB的磁盘空间，每个月15G的带宽流量，正常价每年四十几块钱，赶上活动的话几乎半价就可以购买了。所以我一下买了五六年的了。

这些年这款虚拟主机空间用起来很不错，速度可以接受，几乎没有宕机过，每个月15G的流量也从来没有用完过。但是没想到5月31日博客无法访问了，页面提示如下信息：

Bandwidth Limit Exceeded  
The server is temporarily unable to service your request due to the site owner reaching his/her bandwidth limit. Please try again later.

我登录主机商提供的cPanel面板看了下，流量从3月开始明显增加的。但是为什么会增加就不得而知了，博客早就没有使用谷歌统计和百度统计。我仔细回想下3月份做了什么操作，想来想去发现了3月开始启用了WP Super Cache 插件。我觉得可能是这个原因，于是尝试着停掉WP Super Cache 插件，观察了几天看看，发现流量确实下降了不少。

后来登录cPanel面板发现有个Awstats的统计功能，可以统计网站的访问信息。看了下每个月统计报表发现网站的流量分为浏览器用户流量和非浏览器用户流量，其中大部分是非浏览器流量。非浏览器流量包括搜索引擎机器人，蠕虫病毒产生的流量和非正常的HTTP相应。下面是3月-5月的流量详情：

3月浏览器流量3.28 GB，非浏览器流量5.05 GB  
4月浏览器流量2.37 GB，非浏览器流量5.31 GB  
5月浏览器流量3.94 GB，非浏览器流量8.31 GB

这个时候我才知道网站的流量不仅仅是真正的用户浏览消耗，还有搜索引擎的机器人消耗，而且我的网站大部分的流量反而是机器人消耗的。看了下统计报表发现机器人爬虫中有个叫DotBot是最坏的，它消耗的流量最多，这时我才明白爬虫有好的爬虫也有坏的爬虫。我才想起来robots文件可以限制机器人爬虫的访问，一直以来都是留空的没有配置。上网搜索了下robots.txt怎么配置，摸索了一下，我的配置信息如下：

User-agent: \*  
Disallow: /wp-admin/  
Disallow: /wp-content/  
Disallow: /wp-includes/  
Disallow: /trackback/  
Disallow: /comments/  
Disallow: /attachment/  
Disallow: /comments/feed  
Disallow: /feed  
Disallow: /link  
Disallow: /\*/feed  
Disallow: /\*/comment-page-\*  
Disallow: /\*?replytocom=\*  
Disallow: /\*/trackback  
Disallow: /?s=\*  
Disallow: /\*/?s=\*\\  
Disallow: /wp-\*.php  
User-agent: MJ12bot  
Disallow: /  
User-agent: YisouSpider  
Disallow: /  
User-agent: SemrushBot  
Disallow: /  
User-agent: SemrushBot-SA  
Disallow: /  
User-agent: SemrushBot-BA  
Disallow: /  
User-agent: SemrushBot-SI  
Disallow: /  
User-agent: SemrushBot-SWA  
Disallow: /  
User-agent: SemrushBot-CT  
Disallow: /  
User-agent: SemrushBot-BM  
Disallow: /  
User-agent: SemrushBot-SEOAB  
Disallow: /  
user-agent: AhrefsBot  
Disallow: /  
User-agent: DotBot  
Disallow: /  
User-agent: Uptimebot  
Disallow: /  
User-agent: MegaIndex.ru  
Disallow: /  
User-agent: ZoominfoBot  
Disallow: /  
User-agent: Mail.Ru  
Disallow: /  
User-agent: BLEXBot  
Disallow: /  
User-agent: ExtLinksBot  
Disallow: /  
User-agent: aiHitBot  
Disallow: /  
User-agent: Researchscan  
Disallow: /  
User-agent: DnyzBot  
Disallow: /  
User-agent: spbot  
Disallow: /  
User-agent: YandexBot  
Disallow: /  
User-agent: link  
Disallow: /  
Sitemap: https://www.jfsay.com/wp-sitemap.xml  
Sitemap: https://www.jfsay.com/sitemap.xml

统计报表中有个奇怪的UA名称一个是link一个是feed，我看了网站日志，也没找到名字叫link和feed的。不得而知后问了主机空间的服务商，他说robots.txt只是针对遵守规矩的好蜘蛛，对坏蜘蛛可能没有效果，最好在.htaccess中限制UA的活动，在他的指导下，在.htaccess中添加了如下代码：

rewriteengine on  
RewriteCond %{HTTP\_USER\_AGENT} ^.\*link.\* \[NC,OR\]  
RewriteCond %{HTTP\_USER\_AGENT} ^.\*feed.\* \[NC\]  
RewriteRule .\* – \[F,L\]

又看到cPanel面板有个Webalizer分析工具，它统计出了IP访问网页的数量，我在日志中找到这些IP，看他们到底访问什么内容，发现可疑的就禁止了这些IP访问网站。

这几天一直在观察网站的访问情况，发现流量总算降了下来。看来用robots.txt和.htaccess限制蜘蛛的访问还是很有用的。

**注意：此文中**robots.txt**设置方法已经过时，最佳设置robots.txt的方法如下：[https://www.jfsay.com/archives/2465.html](https://www.jfsay.com/archives/2465.html)**
