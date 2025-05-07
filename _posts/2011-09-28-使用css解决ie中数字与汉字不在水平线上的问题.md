---
title: "使用CSS解决IE中数字与汉字不在同一水平线上的问题"
date: 2011-09-28
categories: 
  - "website"
tags: 
  - "css"
  - "ie"
  - "数字"
  - "汉字"
---

如下的代码：

```
<span class="views"><span id="wp">23</span>次浏览</span>
```

在Chrome和Firefox中的显示效果是：23次浏览。而在IE浏览器中数字“23”会下沉一些（大约1个像素），使得数字与汉字不在同一水平线上，出现略微错位的问题。虽然说不怎么影响浏览效果，但是凡事总得有个解决办法吧。

使用CSS来解决：(也就是在外层span中添加一句代码)

```
.under span.views{vertical-align:middle;}
```

或者把数字和汉字放在一起也可以解决的：

```
<span><span id="wp">23次浏览</span></span>
```
