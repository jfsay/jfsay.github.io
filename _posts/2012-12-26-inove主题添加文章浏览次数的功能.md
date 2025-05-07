---
title: "iNove主题添加文章浏览次数的功能"
date: 2012-12-26
categories: 
  - "website"
tags: 
  - "wordpress"
  - "wp-postviews"
  - "插件"
  - "浏览量"
---

WordPress的iNove主题添加文章浏览次数的功能的效果图：

![views](images/8308604411_1371f5c80e_z.jpg)

大致步骤如下（以下代码针对iNove主题，其他主题的操作过程类似）：

1.安装wp-postviews插件，并设置

2.下载或制作一个浏览量图标view.gif存放到主题的img目录里（如果不需要的话这一步骤可省略）![view](images/8309656374_5c505e3e9c_z.jpg) 

3.修改显示浏览量的页面（index.php、single.php、page.php等）  

<!--more-->

  
找到下面这段代码：

```
<div class="under">		
	<?php if ($options['categories']) : ?><span class="categories"><?php _e('Categories: ', 'inove'); ?></span><span><?php the_category(', '); ?></span><?php endif; ?>
	<?php if ($options['tags']) : ?><span class="tags"><?php _e('Tags: ', 'inove'); ?></span><span><?php the_tags('', ', ', ''); ?></span><?php endif; ?>	
</div>
```

修改为如下的代码：

```
<div class="under">		
	<?php if ($options['categories']) : ?><span class="categories"><?php _e('Categories: ', 'inove'); ?></span><span><?php the_category(', '); ?></span><?php endif; ?>
	<?php if ($options['tags']) : ?><span class="tags"><?php _e('Tags: ', 'inove'); ?></span><span><?php the_tags('', ', ', ''); ?></span><?php endif; ?>
	<span class="views">浏览量:</span><?php if(function_exists('the_views')) { the_views(); } ?>									
</div>
```

4、修改样式表 (style.css)

```
.post .views {
background:url(img/view.gif) no-repeat;
width:16px;
height:16px;
line-height:16px;
display:block;
text-indent:-999em;
}
 
.post .under span.views{
margin-right:6px;
}
```

5、修改侧边栏(sidebar.php)

显示全站所有文章的浏览量：

```
<?php if(function_exists('get_totalviews')) { get_totalviews();} ?>
```

显示热门文章列表（按浏览量的次数排列）

```
<?php get_most_viewed($mode = '', $limit = 10, $chars = 0, $display = true) ?>
```

备注：the\_views()的参数说明

```
<?php the_views($display = true, $prefix = '', $postfix = '', $always = false) ?>
//$display - 直接显示还是作为字符串返回
//$prefix - views前面的内容
//$postfix - views后面的内容
//$always - 是否总是显示（与后台设置中的display options相关
//如果该项为真，则display options无论如何设置都没用）
```
