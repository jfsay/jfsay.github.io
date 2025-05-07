---
title: "Simple Tags相同的tag只显示一次"
date: 2010-10-13
categories: 
  - "website"
tags: 
  - "插件"
---

Simple Tags的Auto Link可以把post文章里出现的Tag关键字自动添加链接，比如我写的上面一句话的Tag是“链接”，那么Simple Tags能够在“链接”两个字上自动添加超链接。

但是有两点缺憾：

- 不支持中文，Tag是中文，不能自动添加链接

- 相同的tag显示多次

解决方法：找到simple-tags/inc/default.options.php文件，修改如下。

对于支持中文Tag：

```
$match = "/\b" . preg_quote($term_name, "/") . "\b/".$case; 
```

修改成：

```
$match = "/" . preg_quote($term_name, "/") . "/".$case; 
```

对于相同的tag只显示一次：

```
if ( preg_match($match, $token) ) { $token = preg_replace($match, $substitute, $token); 
```

修改为:

```
if ( preg_match($match, $token) && (!$must_tokenize)) { $token = preg_replace($match, $substitute, $token,1); 
```
