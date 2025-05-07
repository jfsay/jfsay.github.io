---
title: "分类下的文章不在首页显示，不在RSS中输出的实现"
date: 2011-11-26
categories: 
  - "website"
tags: 
  - "rss"
  - "wordpress"
---

首页文章的显示采用的是循环输出的方式，一般的代码形式如下：

```
<?php if (have_posts()) : while (have_posts()) : the_post();?> 
//文章内容 
<?php endwhile; else : ?> 
<?php endif; ?>
```

从代码可以看到使用的就是while循环来实现文章输出的。

如果想要实现如下功能：某一分类下的文章不在首页显示。这里只需在循环中添加一条跳过语句即可，也就是循环时遇到该分类直接跳过。学习C语言时，我们知道break是“跳出”， continue 是“跳过”，这里需要“跳过不终止”。

分类下的文章不在首页显示操作步骤是：

1、  查看分类ID，在WordPress后台（控制板）进入“分类目录”，鼠标放在欲隐藏的分类名称的链接上，可以看到category&tag\_ID=405，这个数字405就是我们所需要的分类ID。

2、  打开主题目录，地址形式（/public\_html/wp-content/themes/xxoo/），找到index.php文件，在这段代码**后面**添加如下代码：

```
<?php if(in_category('405')) continue; ?>
```

以上方法会产生[首页显示文章数量不正确的问题](http://www.jfsay.com/archives/468.html)，可以采用下面的方法进行第2步操作，方法二如下：

在这段代码**前面**添加如下代码：

```
<?php
if ( is_main_query() && is_home() ) {
	query_posts($query_string . '&cat=-405');
}
?>
```

RSS的一般地址是http://www.jfsay.com/feed，在它的基础上剔除掉某分类下文章即可，也就是http://www.jfsay.com/feed?cat=-405，也就实现了该分类下的文章不在RSS的输出了。
