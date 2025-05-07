---
title: ".htaccess文件保护实例讲解"
date: 2010-06-18
categories: 
  - "website"
tags: 
  - "php"
---

比如说，想要保护admin文件夹，经过以下两个步骤：

步骤一、可以用记事本新建文件.htaccess，输入以下内容：

> AuthType BasicAuth
> 
> UserFile D:/AppServ/www/Hill/admin/.htpasswd
> 
> AuthName "hill"
> 
> require valid-user

各行不多解释，关键是第二行，一定要是绝对路径，表示.htpasswd文件的位置。（位置任意）

然后把这个名为.htaccess的文件放到admin文件夹中。

步骤二、下面就是新建一个名为.htpasswd的文件，名字应该和上面第二行一致。

> 简单的方法：开始-运行-cmd-apache>bin\\htpasswd -c .htpasswd name
> 
> 下面就是输入密码了，是经过md5加密的。

建好后把这个名为.htpasswd的文件放到第二行指定的位置处。

再次说明一下UserFile第二行，花了我好长时间才弄好，如果提示500错误就是路径不正确。对于atbhost空间的位置是/home/注册名。

atbhost空间提供了存放密码的地方：.htpasswds
