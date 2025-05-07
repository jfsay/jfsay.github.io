---
title: "WordPress制作链接页面（网址导航/收藏）的步骤"
date: 2022-11-08
categories: 
  - "software_programming"
tags: 
  - "css"
  - "链接"
---

我也不知道怎么描述这个功能，简单来说就是制作一个纯链接的页面，这个页面分类显示网站的链接，具体效果可以在这里查看[https://www.jfsay.com/links](https://www.jfsay.com/links)

我把需要经常访问的网站聚合在一个页面里，设置为手机浏览器的主页，这样可以方便地访问，不用依赖于浏览器自带的同步功能，这样即使更换浏览器也不影响我使用了。

制作方法如下：

1、将links.php放到主题的目录下

2、后台-页面-新建页面

3、填写标题，内容为空，模板选择Links

这样就可以得到一个显示网址链接的页面了。

[网址书签（收藏夹）主页开发小记](https://www.jfsay.com/archives/1649.html)、[DIV添加超链接小记](https://www.jfsay.com/archives/1650.html)里描述了代码实现的过程，当时是依托于主题样式写的，更换主题又要重新调整，这次稍微修改了代码，把CSS样式直接写在一起，现在是主题无关的，拿下来直接就可以用了。

links.php的代码如下

```
<?php
/*Template Name: Links*/
?>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head profile="http://gmpg.org/xfn/11">
	<meta http-equiv="Content-Type" content="<?php bloginfo('html_type'); ?>; charset=<?php bloginfo('charset'); ?>" />
	<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7" />	
	<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0;" name="viewport" />
	<meta http-equiv="Cache-Control" content="no-transform" />
	<meta http-equiv="Cache-Control" content="no-siteapp" />
	<title>LINKS</title>
	<!-- style START -->
	<!-- default style -->
	<style type="text/css" media="screen">	
	.boxcaption {
	background:#E3E4E6;
	padding:1px 18px;
	border-bottom:1px solid #CCC;
	}
	.boxcaption h3 {
	font-size:12px;	
	font-family:Verdana,"BitStream vera Sans",Tahoma,Helvetica,Sans-serif;
	letter-spacing:0em;
	}
	
	.post .content .linkcat ul{	
	margin:5px 0;padding: 0;	
	}
	.post .content .linkcat ul li {
	list-style:none;
	display: inline-block;
	width:25%;
	padding:2px 0;
	overflow:hidden;	
	margin:5px 0;	
	text-align: center;
	}

	.post .content .linkcat ul li a {
	height:1.2rem;
	line-height:1.2rem;
	text-decoration:none;
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
      </style>
</head>	
<body><!-- wrap START -->
<!-- container START -->
<!-- content START -->
<div id="content">
	<!-- main START -->
	<div id="main_link">
	<?php 
		$linkcats = $wpdb->get_results("SELECT T1.name AS name FROM $wpdb->terms T1, $wpdb->term_taxonomy T2 WHERE T1.term_id = T2.term_id AND T2.taxonomy = 'link_category'");
	?>
	<div class="post" id="post-<?php the_ID(); ?>">
		<div class="content">
			<?php if($linkcats) : foreach($linkcats as $linkcat) : ?>
				<div class="boxcaption"><h3><?php echo $linkcat->name; ?></h3></div>
				<div class="box linkcat">
					<ul>
						<?php							
							$bookmarks = get_bookmarks('orderby=rating & category_name=' . $linkcat->name);
							if ( !empty($bookmarks) ) {

								foreach ($bookmarks as $bookmark) {

									$linkimg = "'".$bookmark->link_url. "'";
									
									echo '<li><div class="nav-icon-normal" id="' . $bookmark->link_id . '" style="background-color:#'. str_pad(pow($bookmark->link_id,3), 6, 'f', STR_PAD_BOTH) .'" onclick="window.location.href='.$linkimg .';return false">' . $bookmark->link_name . '</div><a href="' . $bookmark->link_url . '" title="' . $bookmark->link_description . '">' . $bookmark->link_name . '</a></li>';
								}
							}
						?>
					</ul>
				</div>
			<?php endforeach; endif;  ?>			
		</div>
	</div>	
	<!-- main END -->
</div>
<!-- content END -->
</div>
<!-- container END -->
<!-- wrap END -->
</body>
</html>
```
