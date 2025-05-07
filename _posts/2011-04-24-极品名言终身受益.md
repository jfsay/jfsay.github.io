---
title: "延迟加载图片的实现"
date: 2011-04-24
categories: 
  - "website"
tags: 
  - "inove"
  - "wordpress"
  - "图片"
---

随着文章中图片的增多，拖慢了页面载入速度，本人急需图片的延迟加载。网络上流行最广的是使用jQuery 插件Lazy Load，可参考Lazy Load, 延迟加载图片的 jQuery 插件。

作者介绍丰富，可我还是不清楚该怎么用，也就是不知道该怎么在网站中实施。因为这个jQuery 插件（下载后的文件是jquery.lazyload.js）它只是个js文件并不是Wordpress原生的打包插件，不能通过后台直接上传添加。我连把这个js文件放到网站服务器中的哪里都不知道，请教高人方才知道：“随便你放到哪里，你在要调用的地方写对调用路径就可以了。也就是你想要在wordpress的什么地方调用这个插件了，在哪里调用就在哪里加入插件代码”。

本人使用的是inove模板，现在就介绍一下在inove中实现图片延迟加载的效果的方法。另外，因为是jQuery 插件，所以需要jQuery 库的支持，这里我们使用google托管的js库。

1. 下载 [**jquery.lazyload.js**](https://docs.google.com/leaf?id=0BylPy_4csyrXZWFmNmI5MDEtZWJlMC00MTYzLWJmYTktNzZlYzZjYzc0NDVi&sort=name&layout=list&num=50)（作者Lazy Load [原文介绍及最新版](https://www.appelsiini.net/projects/lazyload/)）

3. 放到主题的js文件夹中（public\_html/wp-content/themes/inove/js）

5. 主题的footer.php中添加如下代码：（public\_html/wp-content/themes/inove/）
    

```
<!-- script START -->
	<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.1/jquery.min.js"></script>	
	<script src="<?php bloginfo('template_url'); ?>/js/jquery.lazyload.js" type="text/javascript"></script>
	<script type="text/javascript">jQuery(document).ready(
	   function($){
              $("img").lazyload({
                  placeholder : "<?php bloginfo('template_url'); ?>/img/ajax-loader.gif",
                  effect      : "fadeIn"
              });
           });
 	</script>
<!-- script END -->
```

在这里，<?php bloginfo('template\_url'); ?>是主题模板的路径，另外我们需要在主题模板的img文件夹中添加一个占位图片（例如ajax-loader.gif），它的作用是，当页面上图片尚未载入时，就显示这张图片。
