---
title: "WP-PostViews插件的函数功能（包含浏览总数）"
date: 2011-11-13
categories: 
  - "website"
tags: 
  - "wordpress"
  - "wp-postviews"
  - "插件"
---

以前文章的浏览量计数使用的是WP-PostViews Plus插件，因为想着在网站里加入[站点统计中的浏览总数功能](https://www.jfsay.com/archives/279.html "WordPress添加站点统计功能")，当时以为WP-PostViews不提供该功能，所以就使用了它的加强版插件。

这几天发现文章计数总出现问题，刚发布的文章访问数就立马飙升（可能是网络爬虫的访问数也计算在内了），我也没有细究，于是拿出[WP-PostViews插件](http://wordpress.org/extend/plugins/wp-postviews/)来研究。

WP-PostViews的函数在wp-postviews/wp-postviews.php里，通过函数名大致可以猜测其功能了。下面就让我们来细数一下它的主要函数功能。

the\_views()是最主要的函数，显示文章的浏览次数。

get\_least\_viewed()显示最少被浏览的文章列表，包括文章或页面。

get\_most\_viewed()显示最多被浏览的文章列表，包括文章或页面。

get\_least\_viewed\_category()显示某个分类下最少被浏览的文章列表，包括文章或页面。

get\_most\_viewed\_category()显示某个分类下最多被浏览的文章列表，包括文章或页面。

get\_most\_viewed\_ tag()显示某个标签下最多被浏览的文章列表，包括文章或页面。

get\_least\_viewed\_tag()显示某个标签下最少被浏览的文章列表，包括文章或页面。

get\_totalviews()显示浏览总数。

snippet\_text()显示按要求截取文本片段。

这些函数中，我觉得用的最多的应该是the\_views()，它用来显示文章的流量次数，你可以把下面这段代码添加到主题下的post.php和index.php中：

```
<?php if(function_exists('the_views')) { the_views(); } ?>
```

因为该插件提供Widget的小工具，其他的几个显示最多/最少文章列表的函数不用手工添加。

get\_totalviews()函数可以显示整个站点的浏览总数，你可以在网站合适的位置添加下面的代码：

```
<?php if(function_exists('get_totalviews')) { get_totalviews();} ?>
```

当然上述的函数可以通过修改参数来实现不同的功能。
