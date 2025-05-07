---
title: "WordPress作者评论的名称后面添加「作者」的文本标识"
date: 2023-10-16
categories: 
  - "website"
tags: 
  - "wordpress"
---

标题比较拗口，举例说明如下：假如作者名称是ABC，默认的作者评论是ABC说：ZZZ。想要实现的效果是ABC（作者）说：ZZZ。也就是在作者的名称后面加了「作者」的提示，这样当评论比较多时可以很快发现哪条是作者的评论。

下面是网上的找来的实现方法，我做了一点修改，只需将代码放到主题的模板函数文件里 (functions.php)就行了。

```
if ( ! class_exists( 'WPB_Comment_Author_Role_Label' ) ) :
class WPB_Comment_Author_Role_Label {
public function __construct() {
add_filter( 'get_comment_author', array( $this, 'wpb_get_comment_author_role' ), 10, 3 );
add_filter( 'get_comment_author_link', array( $this, 'wpb_comment_author_role' ) );
}
 
//Get comment author role 
function wpb_get_comment_author_role($author, $comment_id, $comment) { 
$authoremail = get_comment_author_email( $comment); 
//Check if user is registered
if (email_exists($authoremail)) {
$this->comment_user_role = "（作者）";
} else { 
$this->comment_user_role = '';
} 
return $author;
} 
 
//Display comment author                   
function wpb_comment_author_role($author) { 
return $author.= $this->comment_user_role; 
} 
}
new WPB_Comment_Author_Role_Label;
endif;
```

Update：发现了一个更简单的方法，只需要修改CSS样式就能实现这样的功能，只需找到作者的评论，用CSS伪元素就行了，下面是我的使用的代码：

```
.bypostauthor > .comment-body > .comment-meta > .comment-author > .fn:after { 
    content: "作者";
    background: #FF1100;
    color: white;    
    margin: 0 3px;
    border-radius: 3px;
    font-size: 8px;
    padding: 1px 2px;
    vertical-align: middle;
}    
```
