---
title: "DIV添加超链接小记"
date: 2020-05-25
categories: 
  - "software_programming"
tags: 
  - "css"
  - "链接"
---

[接上篇](http://www.jfsay.com/archives/1649.html)，已经实现了上面是纯文字“图片”下面是文字的效果，但是有个问题是“图片”没有超链接，点击没反应，体验不太好，于是想着把“图片”（实际是文字）加上超链接。最简单的方法是加<a>标签，但是测试后发现点击链接的瞬间图片中的文字会变色，而且会有下划线。然后想着能不能给“图片”外的整个DIV加超链接，发现可以通过通过window.location.href函数来实现：

```
<div onclick="window.location.href= 'www.baidu.com';return false">在当前窗口跳转至百度</div>
```

看起来很简单，但是我在这里摸索了好长时间，问题就出在PHP的echo输出不能有嵌套单引号。

echo的输出一般是这样：echo ' <div></div> ' ;

单引号里面再嵌套单引号会报错，如下：

```
echo  ' <div onclick="window.location.href= 'www.baidu.com';return false"> ' ;
```

我试图去掉单引号或者把单引号改成双引号，发现不会报错了，但是点击不会跳转。

后来的解决办法是把单引号的内容放在变量里，这样形式上echo里没有嵌套单引号了，问题得到解决。把$bookmark->link\_url加上单引号放到linkimg里，代码如下：

```
$linkimg = "'".$bookmark->link_url. "'";

echo '<li><div class="nav-icon-normal" id="' . $bookmark->link_id . '" style="background-color:#'. str_pad(pow($bookmark->link_id,3), 6, 'f', STR_PAD_BOTH) .'" onclick="window.location.href='.$linkimg .';return false">' . $bookmark->link_name . '</div><a href="' . $bookmark->link_url . '" title="' . $bookmark->link_description . '">' . $bookmark->link_name . '</a></li>';
```
