---
title: "网址书签（收藏夹）主页开发小记"
date: 2020-05-22
categories: 
  - "software_programming"
tags: 
  - "css"
  - "php"
  - "主页"
  - "链接"
---

从Chrome诞生起就用了，到现在有十几年了，无奈Google在国内是不存在的，Chrome无法同步数据包括网址书签，每回换电脑和手机都要手工加一堆书签便于访问，好在常用的不多，也就十几个，加起来也不难，所以一直也没想到解决书签同步的问题。

前几天突然想为什么自己不做个书签主页，类似于导航网站那样，把经常访问的网址放在浏览器主页。

我想着找一个现成的导航网站源码，然后挂到虚拟主机空间里，再绑定一个子域名。找来找去，都是臃肿的，没有合适的。

后来想着WordPress自带链接页，何不把这个链接页改造一下呢。

我用的WordPress主题是inove，差不多有十年了，大大小小的修改很多，也不想去折腾了。但是inove诞生的时候没有考虑手机浏览的问题，只能自己动手把links页面给改造成手机和PC都能友好访问的页面。

在网站HTML文件的开头，增加viewport meta标签告诉浏览器视口宽度等于设备屏幕宽度，且不进行初始缩放。代码如下：

```
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0;" name="viewport" />
```

然后把页面中固定宽度的删除，再删除掉head和foot，下面就是不断的调整css的样式了，调一点看下效果，模样初现了。

只显示链接文字，Jasmine说太单调，辨识度不高，于是想在链接上面加个图片，实现的效果是图片在上，下面显示网址标题及链接。图片直接取网站favicon的图标，如下：

```
<img src="', $bookmark->link_url , '/favicon.ico" onerror="this.src=img/wp-logo.png "/>
```

实际发现好多问题：1、加载缓慢。2、好多网址取不到favicon.ico。3、由于网络及缓存原因，有时能取到有时取不到favicon.ico

于是干脆不要favicon.ico了，直接用纯文字的首字作为图片，为了提高辨识度，“图片”的背景色要不一样。

HTML部分的代码如下：

```
<div class="content">
			<?php if($linkcats) : foreach($linkcats as $linkcat) : ?>
				<div class="boxcaption"><H6><?php echo $linkcat->name; ?><h6></div>
				<div class="box linkcat">
					<ul>
						<?php
							$bookmarks = get_bookmarks('orderby=rating & category_name=' . $linkcat->name);
							if ( !empty($bookmarks) ) {
								foreach ($bookmarks as $bookmark) {
									echo '<li><div class="nav-icon-normal" id="' . $bookmark->link_id . '" style="background-color:#'. str_pad(pow($bookmark->link_id,3), 6, 'f', STR_PAD_BOTH) .'" >' . $bookmark->link_name . '</div><a href="' . $bookmark->link_url . '" title="' . $bookmark->link_description . '">' . $bookmark->link_name . '</a></li>';
								}
							}
						?>
					</ul>
					<div class="fixed"></div>
				</div>
			<?php endforeach; endif; //the_content(); ?>
			<div class="fixed"></div>
</div>
```

CSS样式如下：

```
/* linkcat START */
.post .content .linkcat ul li {
	list-style:none;
	float:left;
	width:25%;
	padding:2px 0;
	overflow:hidden;	
	margin:5px 0;	
	text-align: center;
}
.post .content .linkcat ul li a {
	padding-left:22px;*/
	height:1.2rem;
	line-height:1.2rem;
}
.nav-icon-normal {
       width: 32px;
       height: 32px;
       line-height: 33px;
       display: inline-block;
       border-radius: 6px;
       background-color: #b3b4c5;
       vertical-align: middle;
       overflow: hidden;
       font-size: 16px;
       text-indent: 8px;
       text-align: center;
       letter-spacing: 8px;
       color: #fff;
       word-break: break-all;
       display: block;
       margin: 0 auto;
}
/* linkcat END */
```

核心代码如下：

```
echo '<li><div class="nav-icon-normal" id="' . $bookmark->link_id . '" style="background-color:#'. str_pad(pow($bookmark->link_id,3), 6, 'f', STR_PAD_BOTH) .'" >' . $bookmark->link_name . '</div><a href="' . $bookmark->link_url . '" title="' . $bookmark->link_description . '">' . $bookmark->link_name . '</a></li>';
```

纯文字的首字图片背景颜色取得是链接的id，然后补全成6位十六进制颜色，这里用了这个函数str\_pad($string, 6, 'f', STR\_PAD\_BOTH)，用f来补充。因为id很接近，为了更好的区分颜色，我用了pow(x,y)函数把id的数字扩大化，最终使用的函数是str\_pad(pow($bookmark->link\_id,3), 6, 'f', STR\_PAD\_BOTH)

因为多次修改HTML页面，可能会有HTML标签不闭合的问题，推荐使用在线的HTML标签闭合检测工具来检查下页面代码。

[点击查看我做出来的链接页效果](http://www.jfsay.com//links)

PS. 链接的排序用的是orderby=rating，评分低的在前面。
