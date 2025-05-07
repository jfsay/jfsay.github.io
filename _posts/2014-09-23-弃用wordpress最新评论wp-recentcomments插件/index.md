---
title: "弃用WordPress最新评论WP-RecentComments插件"
date: 2014-09-23
categories: 
  - "website"
tags: 
  - "wordpress"
  - "博客"
---

从博客建站伊始用了好多MG12的插件，其中就包括侧边栏显示最新评论的WP-RecentComments插件。WordPress自带的最新评论过于简陋，只显示某人在某篇文章有评论，连评论的摘要都没有，每次还要点进去才能看到人家说了什么。

WP-RecentComments很强大，可以显示评论作者的Gravatar头像，评论日期和摘要，而且可以翻页显示之前的评论内容。

正是因为它过分地强大了，我才会舍弃它。它的好些功能我并不需要，我只需要在侧边栏显示评论的摘要即可。而且我发现它的一个缺点是页面载入时评论内容会延迟好久才能载入，拖慢了网站的速度。

下面是网上流传的侧边栏显示最新评论的代码，经过我的需求稍微做了修改，放到侧边栏的sidebar.php就可以了。

```
<ul>
   <?php
      global $wpdb;
      $sql = "SELECT DISTINCT ID, post_title, post_password, comment_ID,comment_post_ID,      comment_author,comment_author_email,comment_date_gmt, comment_approved, comment_type,comment_author_url, SUBSTRING(comment_content,1,20) AS com_excerpt FROM $wpdb->comments LEFT OUTER JOIN $wpdb->posts ON ($wpdb->comments.comment_post_ID = $wpdb->posts.ID) WHERE comment_approved = '1' AND post_password = '' AND comment_author != '".$outer."' ORDER BY comment_date_gmt DESC LIMIT 15";
      $comments = $wpdb->get_results($sql);
      $output = $pre_HTML;
      foreach ($comments as $comment) {
          $output .= "\n<li><a href=\"" . get_permalink($comment->ID) . "#comment-" . $comment->comment_ID . "\" title=\"". $comment->comment_date_gmt . " post by " . $comment->comment_author . "\">" . strip_tags($comment->com_excerpt) ."</a></li>";
      }
      $output .= $post_HTML;
      echo $output;
   ?>
</ul>
```

我去掉了comment\_type = ''（只显示评论，不显示pingback和trackback类评论）和user\_id=''（不显示博主），如果你需要可以把它们加到WHERE的条件中。

UPDATA:该方法使用SQL语句操作数据库的代码来实现，并不是WordPress官方推荐的方式，最好使用WordPress自带函数实现上述功能，详见[代码实现侧边栏最新评论的功能](http://www.jfsay.com/archives/875.html)。
