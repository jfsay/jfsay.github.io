---
title: "开始使用WordPress子主题"
date: 2022-11-23
categories: 
  - "website"
tags: 
  - "wordpress"
  - "主题"
---

新的主题安装好以后或多或少会对它进行修改，但是当主题更新以后修改的内容就会被覆盖丢失了，WordPress早就考虑到这个问题，那就是子主题。

除非你安装的主题永远不会更新，不然尽快使用子主题吧，建议安装完新主题后立即创建子主题。

创建子主题的方法：

一、通过WordPress万能的插件，比如Child Theme Configurator，创建完成子主题就可以把插件删除了。

二、手工创建，下面说下手工创建的步骤

假设原主题的名字是ABC

1.在themes目录新建一个文件夹ABC Child（和ABC在同一级目录）

2.在ABC Child下新建style.css文件

3.在style.css文件中添加以下内容：

```
/*Theme Name: ABC ChildTemplate: ABC*/
```

4.这样子主题也就创建完成了，启用子主题

5.以后如果改动原主题中任何的内容，只要在ABC Child新建同名文件就行了。简单的方法是复制一份文件到ABC Child中，然后再修改这份文件。

6.模板函数 (functions.php)是个例外，子主题的functions.php和原主题是同时生效的，也就是说原主题的functions.php里的内容不要出现在子主题中，子主题functions.php一开始是空白的，只新增修改的内容。
