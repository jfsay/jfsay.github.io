---
title: "升级WordPress3.8小记"
date: 2014-02-07
categories: 
  - "website"
tags: 
  - "wordpress"
---

忍受了好几个月WordPress后台更新版本信息的干扰，今天终于把WordPress从3.6版本升级到3.8.1，中间跳过了好几个版本更新。

这次更新并不是一帆风顺的，做了不少的工作。

1、禁用自动保存、自动草稿、自动修订功能

到目前为止还没有出现禁用WordPress自动保存、自动草稿、自动修订功能的完美方法，每一次更新都需要修改WordPress根目录下的wp-admin/includes/post.php文件来[实现文章ID连续](http://www.jfsay.com/archives/136.html "WordPress禁用自动保存、自动草稿和修订版本功能（ID连续）")，这也是我为什么不积极对WordPress进行更新的原因。

网络上出现了针对WordPress3.8的新方法，通过修改Theme对应的functions.php文件。具体实现步骤是找到functions.php文件，在“< ?php之后”或“？>”之前插入如下的代码：

```
function keep_id_continuous(){
	global $wpdb;
	$lastID = $wpdb->get_var("SELECT ID FROM $wpdb->posts WHERE post_status = 'publish' OR post_status = 'draft' OR post_status = 'private' OR ( post_status = 'inherit' AND post_type = 'attachment' ) ORDER BY ID DESC LIMIT 1");
	$wpdb->query("DELETE FROM $wpdb->posts WHERE ( post_status = 'auto-draft' OR ( post_status = 'inherit' AND post_type = 'revision' ) ) AND ID > $lastID");
	$lastID++;
	$wpdb->query("ALTER TABLE $wpdb->posts AUTO_INCREMENT = $lastID");
}
// 将函数钩在新建文章、上传媒体和自定义菜单之前。
add_filter( 'load-post-new.php', 'keep_id_continuous' );
add_filter( 'load-media-new.php', 'keep_id_continuous' );
add_filter( 'load-nav-menus.php', 'keep_id_continuous' );
// 禁用自动保存，所以编辑长文章前请注意手动保存。
add_action( 'admin_print_scripts', create_function( '$a', "wp_deregister_script('autosave');" ) );
// 禁用修订版本
remove_action( 'pre_post_update' , 'wp_save_post_revision' );
```

2、弹出“blockui requires jquery v1.2.3 or later you are using v1.10.2”的对话框

原因是WordPress的某个插件的JS中使用了jQery.BlockUI的版本太旧，解决方法是逐个排查你所使用的插件，替换掉该插件JS中过久的jQery.BlockUI代码片段。我的问题出现在Quick Comments插件身上。

> My plugin used a file called wf-an-jqery-plugins.js. Inside that file was a chunk of jQery.BlockUI code that said it was v2.39.
> 
> I went to the following link for the latest jQuery.BlockUI code (v2.64) and then just replaced the v2.39 code in that plugin file with the code from this link. Hey presto, it all works again:http://malsup.github.io/jquery.blockUI.js

3、wpdb::prepare() 报错

我的报错位置是博客最下面的footer的地方，报错的内容为“Warning: Missing argument 2 for wpdb::prepare(), called in footer.php on line 75 and defined in /www/wp-includes/wp-db.php on line 990”。

解决方法是找到prepare()函数出现的地方，为它增加一个内容为空的参数：在footer.php中找到

```
$wpdb->prepare('xxx')
```

 改为

```
$wpdb->prepare('xxx', '')
```

4、更新并精简了一些`WordPress插件，可以查看我的[WordPress插件列表](http://www.jfsay.com/archives/251.html "我的WordPress插件列表")。`
