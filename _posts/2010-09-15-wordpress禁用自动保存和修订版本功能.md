---
title: "Wordpress禁用自动保存、自动草稿和修订版本功能（ID连续）"
date: 2010-09-15
categories: 
  - "website"
tags: 
  - "id"
  - "wordpress"
---

我的博客文章的固定链接地址是采用文章ID作为Permalink的，昨天却发现相邻两篇文章的ID相差很远，有的离谱的差了几十个。

Google一下才知道，wordpress具有版本修订（Post Revisions）、自动草稿（Auto-Draft）和自动保存（Auto-Save）的功能。版本修订是如维基百科似的，使得修订的文章具有版本记录。自动保存的作用也是很显然的。可是，日志的版本修订功能Revision占用ID，同样地自动保存功能也占用ID，这样你为一篇文章编辑很多次或者写一篇很长的文章，在数据库中会保存多个不同ID的记录，最终发表的文章ID当然也就是不连续的了。

解决这个问题，我是用的方法是采用[disable revisions and autosave](http://exper.3drecursions.com/2008/07/25/disable-revisions-and-autosave-plugin/)插件。同时月光介绍了wordpress 3.0.1出现的[新问题](http://www.williamlong.info/archives/2301.html)：

> 只要新建一篇日志，即使不写内容，数据库中也会自动保存一篇草稿。

解决：编辑wp-admin/includes/post.php文件，找到以下两条语句：

```
$post_id = wp_insert_post( array( 'post_title' => __( 'Auto Draft' ), 'post_type' => $post_type, 'post_status' => 'auto-draft' ) );
$post = get_post( $post_id );
```

替换为以下代码：

```
$post_auto_draft = $wpdb->get_row( "SELECT * FROM $wpdb->posts WHERE post_type = '$post_type' AND post_status = 'auto-draft' LIMIT 1" );
if ( $post_auto_draft ) {
    $post = $post_auto_draft;
} else {
    $post = get_post( wp_insert_post( array( 'post_title' => __( 'Auto Draft' ), 'post_type' => $post_type, 'post_status' => 'auto-draft' ) ) );
}
```

对于日志ID已经出现混乱的问题，可以直接进入phpadmin中手动调整的。

对于梳理成连续的ID，继续发表新文章的时候，ID还是会从之前不连续的数字之后开始起跳的问题，解决方法是：

> 在phpmyadmin里的数据库执行一行SQL命令：
> 
> alter table wp\_posts AUTO\_INCREMENT=n
> 
> 其中n为你想新开始的数字，比如把多余的修订删完之后，最后一篇ID为20，此时n为21。
