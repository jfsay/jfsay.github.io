---
title: "简单的PHP相关文章链接的实现方法"
date: 2010-08-02
categories: 
  - "website"
tags: 
  - "php"
---

一般文章的正文后面会跟上该文章的相关文章，罗列一条条相似的文章。这种做法不仅对于作者还是读者都是有利的，既可以吸引粘连读者又可以使读者加深阅读。

对于PHP编程实现来说，一般的方法是在写文章时自己添加或者自动生成Tag标记，之后再寻找这些Tag相关性高的文章。谷歌实验室的Google Related Links同样也可以实现此功能，有兴趣的同学可以前往研究，不过需要申请。

我们知道文章标题能够涵盖文章的大体要义（标题党除外），相关文章在标题上也会有一定的相似度。下面就来介绍一种基于文章标题Tilte的相关文章实现方法，其实也就是利用了PHP自身带的similar\_text函数来判断内容的相似度。

```
<?php
require('conn.php');
$sql="select title from content order by id"; //判断标题相似度
$result=mysql_query($sql,$conn); 
 
while($row=mysql_fetch_array($result)){
similar_text($row['title'], $title, $percent); //比较相似度 存放于$percent
if($percent>30 && $percent<100){echo $row['title'];} //相似度高于30小于100，小于100就是排除掉自己。当然这个值可以根据实际来修改。
}
?>
```

这样的话就可以把和该文章标题相似度在30-100间的文章标题输出了。
