---
title: "文章添加链接与版权的非插件实现"
date: 2010-11-26
categories: 
  - "website"
tags: 
  - "wordpress"
---

为WordPress添加链接与版权，可以通过Add Post URL插件来实现此功能。可是Wordpress大牛们给的建议是，能不用插件就不要使用插件。所以我们来看一下非插件的实现方法。

先介绍一下需要的几个Wordpress函数。

```
<?php bloginfo('url'); ?>  //博客链接，如http://www.jfsay.com
<?php bloginfo('name'); ?> //博客名称，如静风博客
<?php the_permalink(); ?>   //文章链接，如http://www.jfsay.com/archives/204.html
```

下面就来使用上面的函数，在文章内容下添加链接与版权。当然添加的位置你可以随意定。具体的方法是：

找到主题中的文章页（single.php），然后找到其中的<?php the\_content(); ?>，在其下面添加如下的代码：

```
<div style="margin-top: 20px; font-style: Arial"><p><strong>原创文章，转载请注明：</strong> 转载自<a href=<?php bloginfo('url'); ?> ><?php bloginfo('name'); ?></a>[<a href=<?php bloginfo('url'); ?>><?php bloginfo('url'); ?></a>]</p><p><strong>本文链接地址:</strong> <a href=<?php the_permalink() ?>><?php the_permalink() ?></a></p></div>
```

具体的效果如下：

**原创文章，转载请注明：** 转载自[静风博客](https://www.jfsay.com/)\[[http://www.jfsay.com](https://www.jfsay.com/)\]

**本文链接地址****:** [http://www.jfsay.com/archives/204.html](https://www.jfsay.com/archives/204.html)
