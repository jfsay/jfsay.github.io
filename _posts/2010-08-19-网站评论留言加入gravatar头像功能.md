---
title: "网站评论留言加入Gravatar头像功能"
date: 2010-08-19
categories: 
  - "website"
tags: 
  - "gravatar"
  - "头像"
---

在浏览别人的网站以及Blog总会发现其成员列表或者评论头像的异彩纷呈，尤其是WordPress搭建的网站更是如此，这其实是通过Gravatar来实现的。Gravatar，全称Globally Recognized Avatar（全球通用头像）。如果在Gravatar的服务器上放置了你自己的头像，那么当你到任何一个支持 Gravatar的网站留言时，这个网站都就会根据你所提供的Email地址为你显示出匹配的头像。目前WordPress已经自带了Gravatar头像功能，大部分的Wordpress使用者都会开通这个Gravatar头像功能。所以当你在这些网站留言的时候，都会显示你的Gravatar头像。

也就是说这些头像是放在Gravatar上的，它与电子邮件地址关联，当你提供了邮件地址也就同时给出了对应的头像了。简单说一下Gravatar头像实现的原理（其实自己[注册一下](http://en.gravatar.com/site/setup)，原理也就很明白了）。用电子邮件地址：Email Address: 123@example.com注册，系统会采用MD5来加密产生Email Hash: 81c793bc7cc255679d90c4518784b1f，然后通过http://www.gravatar.com/avatar/81c793bc7cc255679d90c4518784b1f?s=40来访问头像。

我们可以用下面的代码测试一下：

```
<?php 
$email="123@example.com";//注册的邮箱地址
echo '<img alt="Gravatar Icon" src="http://www.gravatar.com/avatar/'.md5($email).'?s=40" />'; 
?>
```

如果注册成功的话，就会显示你所上传的图片了。?s=40为显示图片的边长参数。

具体的网站实施就是把上面的代码稍作修改，替换掉原有的显示头像的"<img />"即可。

PS:寻找在网站上实现Gravatar头像的方法或代码，一窝蜂的都是WordPress的插件或者代码实现，看来现在WordPress真的很是流行。
