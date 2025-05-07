---
title: "CSS实现背景颜色与边框距离（空隙）"
date: 2010-07-12
categories: 
  - "website"
tags: 
  - "css"
---

Gmail的登录框淡蓝色的外框和淡灰色的内容背景间有一段白色的空隙，可以使用内外两层容器实现，外层为背景：

```
#bg {border: 1px solid green; 
width: 300px; 
margin-left:auto; margin-right:auto;
padding: 2px; 
font-weight: bold; 
background-color:#fff;}
```

内层为内容：

```
#content{
height:100%;
background-color:#DDDEEA;
padding: 10px;
}
```

HTML实现为：

```
<div id="bg">
<div id="content">
 中间的内容
</div>
</div>
```
