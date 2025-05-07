---
title: "Inove使用WP-RecentComments"
date: 2010-12-06
categories: 
  - "website"
tags: 
  - "插件"
---

WP-RecentComments是MG12写的一个最新评论插件，可以显示评论者的头像、名字以及内容。评论内容默认是折叠收起的，可以通过点击来展开，这样使得不需要进入页面就能查看完整的评论了。另外还有翻页的功能，可以查看更多的评论。

可是Inove使用最新版的WP-RecentComments总是出现样式混乱的问题：

- 头像在上，名字和评论在头像下面。（我们需要的是头像在左，名字和评论在右）

- 每条评论前面出现“点”。

具体的原因我没有细究，觉得应该是CSS调用的问题。于是拿出来wp-recentcomments/wp-recentcomments.php文件，发现其中的调用CSS语句中有一个判断是使用模板CSS还是插件CSS。觉得是这个判断没有起作用，反正我是想使用插件的CSS的，干脆把第一个if注释掉。方法是：

```
if($options['use_css']) {
	if(file_exists(TEMPLATEPATH . '/wp-recentcomments.css')){
		wp_enqueue_style('wp-recentcomments-custom', get_bloginfo('template_url') . '/wp-recentcomments.css', array(), $plugins_version, $plugins_css_media);
	} 
        else {
	       wp_enqueue_style('wp-recentcomments', $plugins_css_url . '/wp-recentcomments.css', array(), $plugins_version, $plugins_css_media);
	}
}

```

修改为：

```
wp_enqueue_style('wp-recentcomments', $plugins_css_url . '/wp-recentcomments.css', array(), $plugins_version, $plugins_css_media);

```

这样就可以调用插件的CSS了，解决了头像和评论的位置问题。

第二个问题的解决是，在主题的style.css文件中添加如下代码：

```
#sidebar .rc-item, #sidebar .rc-navi{background:transparent;line-height:145%;padding:2px 0;}

```
