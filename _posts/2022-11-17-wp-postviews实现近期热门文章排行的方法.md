---
title: "WP-PostViews实现近期热门文章排行的方法"
date: 2022-11-17
categories: 
  - "website"
tags: 
  - "wp-postviews"
---

WP-PostViews是按文章的浏览量显示最多/最少文章，但是没有限定时间，浏览量是全站文章统计的，这就存在一个问题：先发布的文章由于时间更久，浏览量累计起来更大，所以热门文章排行很久就不会产生变化。

据说WP-PostViews以前的版本提供了get\_timespan\_most\_viewed这个函数来实现设定日期的文章排行，之后这个函数取消了。

2019年在WP-PostViews插件的讨论中，有人提出“Display most viewed posts in some period of time”，不过插件作者的答复是“This option was never possible because the plugin only stored accumulated post views.”作者有点不负责任地答非所问，即使「插件仅存储累计的帖子浏览量」，也可以实现给定时间内的文章排行啊。

我在浏览其他的帖子中发现了这个问题的解决方法，只需增加几行代码就行了，步骤如下：

1、找到WP-PostViews插件下的wp\_postviews.php文件

2、找到Display Most Viewed Page/Post的get\_most\_viewed函数

3、在$most\_viewed = new WP\_Query( array( ) ); 中添加以下代码：

```
'date_query' => array(
'after' => '1 year ago',
),
```

你可以按需将时间参数改为1 week ago、1 month ago等。

不过，这种方法有个问题，当插件升级后修改的内容会丢失，需要重新添加代码。
