---
title: "WordPress添加站点统计功能"
date: 2011-05-06
categories: 
  - "website"
tags: 
  - "wordpress"
  - "博客"
---

WordPress具有统计功能的插件着实不少，大部分功能都很强大，包括记录访客登录时间、次数、IP、访问页、点击率等等，有的号称比Google analytics还强大。可是如果只需要简单的功能，显示站点的文章数、评论数、浏览数、链接数等几项数据，在前台展示给访客看的话，WordPress自带的函数大体上能实现上述功能。

<!--more-->

代码如下：

```
<div class="widget">		
    <h3>站点统计</h3>
    <ul>	
	<li>文章总数：<?php $count_posts = wp_count_posts(); echo $published_posts = $count_posts->publish;?></li>
	<li>评论总数：<?php echo $wpdb->get_var("SELECT COUNT(*) FROM $wpdb->comments");?></li>
	<li>链接总数：<?php $link = $wpdb->get_var("SELECT COUNT(*) FROM $wpdb->links WHERE link_visible = 'Y'"); echo $link; ?></li>
	<li>标签总数：<?php echo $count_tags = wp_count_terms('post_tag'); ?></li>
	<li>浏览总数：<?php if(function_exists('the_views')) { get_totalviews();}?></li>	
    </ul>		
</div>
```

这里的“浏览总数”使用的是WP-PostViews Plus的统计所有浏览量的函数get\_totalviews()（个人觉得这个函数可以当作网站计数器来使用），故而需要安装此插件，其他的函数皆为WordPress自带的函数。

其他的WordPress相关函数还有：

```
草稿总数：<?php $count_posts = wp_count_posts(); echo $draft_posts = $count_posts->draft; ?>
运行时间：<?php echo floor((time()-strtotime("2012-12-12"))/86400); ?>
页面总数：<?php $count_pages = wp_count_posts('page'); echo $page_posts = $count_pages->publish; ?>
分类总数：<?php echo $count_categories = wp_count_terms('category'); ?>
```
