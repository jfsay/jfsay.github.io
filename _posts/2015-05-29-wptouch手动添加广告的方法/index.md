---
title: "WPtouch手动添加广告的方法"
date: 2015-05-29
categories: 
  - "website"
tags: 
  - "wordpress"
  - "wptouch"
  - "插件"
---

WPtouch是一款很流行的WordPress移动版（手机版）主题插件，它能够自动识别移动设备，调用插件自带的移动版主题，实现页面的自适应大小——也就是说安装了WPtouch之后你不必考虑细节就拥有了一套手机版的网站了。

WPtouch分为免费版和收费版，免费版的功能对于一般的博客已经够用了，只是之后作者版本升级去掉了广告支持的功能，这对于玩广告的博主来说无疑是一大损失。如果WPtouch免费版加上广告功能就两全其美了。

下面介绍如何在WPtouch免费版添加广告功能的方法，其实也就是修改插件主题目录下的文件，添加上代码片段即可。**该方法的缺点是插件升级的话修改的内容就被覆盖掉了，需要重新添加广告代码。**

1、进入WPtouch插件的主题目录：/wp-content/plugins/wptouch/themes/bauhaus/default/

2、根据需要修改目录下的文件，我这里修改header-bottom.php和single.php两个文件，一个是主页面，一个是文章页面。

header-bottom.php在以下代码中添加广告代码片段，效果是在主页的导航栏的下面显示广告。

```
<?php if ( is_home() ) { ?>
	<!-- 广告代码片段-->
		<?php if ( function_exists( 'foundation_featured_slider' ) ) { ?>
			<?php foundation_featured_slider(); ?>
		<?php } ?>
	<?php } ?>
```

single.php在以下代码的上面和下面分别添加广告代码片段，效果是在文章正文的上下显示广告。

```
<!--广告代码片段-->
<div class="post-page-content">
	<?php if ( bauhaus_should_show_thumbnail() && wptouch_has_post_thumbnail() ) { ?>
		<div class="post-page-thumbnail">
			<?php the_post_thumbnail('large', array( 'class' => 'post-thumbnail wp-post-image' ) ); ?>
		</div>
	<?php } ?>
        <?php wptouch_the_content(); ?>
<!-- 广告代码片段-->
```
