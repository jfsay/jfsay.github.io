---
title: "代码实现侧边栏最新评论的功能"
date: 2015-05-24
categories: 
  - "website"
tags: 
  - "wordpress"
  - "博客"
---

WordPress自带的侧边栏最新评论何其丑陋，就给个标题扔个链接，连评论内容都看不到。于是我早早地使用了华丽的WP-EasyArchives来实现最新评论功能，可是这个插件的好多东西我并不需要，而且插件经常失灵，评论内容加载又很缓慢，于是我就弃插件而不用[使用代码](http://www.jfsay.com/archives/974.html)来实现最新评论的功能了。

只是《[弃用WordPress最新评论WP-RecentComments插件](http://www.jfsay.com/archives/974.html)》中提到的代码使用SQL语言调用数据库数据来实现，感觉并不友好，于是改用WordPress自带函数来实现了。具体的代码如下： 

```
<h2>最新评论</h2>
	<ul>
		<?php
			$show_comments = 15; //评论数量
			$i = 1;
			$comments = get_comments('number=50&status=approve&type=comment'); //取得前50个评论
			foreach ($comments as $rc_comment) { ?>
			<li><a href="<?php echo get_permalink($rc_comment->comment_post_ID); ?>#comment-<?php echo $rc_comment->comment_ID; ?>" title="<?php echo $rc_comment->comment_date_gmt; ?> post by <?php echo $rc_comment->comment_author; ?>"><?php echo mb_strimwidth(strip_tags($rc_comment->comment_content),0,43,"..."); ?></a></li>
			<?php
			if ($i == $show_comments) break; //评论数量达到退出遍历
			$i++;	
			} //End foreach
		?>
	</ul>
```

把上述代码扔到侧边栏就可以了。

注：get\_comments()为获取评论内容，mb\_strimwidth()为截取字符串输出，strip\_tags()为清空HTML标记。
