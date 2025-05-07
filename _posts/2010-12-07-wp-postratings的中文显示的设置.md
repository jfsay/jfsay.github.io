---
title: "WP-PostRatings的中文显示的设置"
date: 2010-12-07
categories: 
  - "website"
tags: 
  - "插件"
---

WP-PostRatings是一款Wordpress的文章评分插件，评分形式多样，功能丰富，小巧简单，足够强大。然而，插件的显示语言是英文的，这对中文博客来说不是太友好。不过中文的显示的设置也十分简单，下面简要介绍一下。

评分显示出要是在Post Rating Templates中设置的。

Ratings None:评分前的显示

%RATINGS\_IMAGES\_VOTE% (欢迎评分)

Ratings Voted Text:评分后的显示（评分人可见）

%RATINGS\_IMAGES% (<em>共<strong>%RATINGS\_USERS%</strong> 次打分, 平均得分: <strong>%RATINGS\_AVERAGE%</strong> </em>)

Ratings Vote Text:评分后的显示（非评分人可见）

%RATINGS\_IMAGES\_VOTE% (共<strong>%RATINGS\_USERS%</strong> 次打分, 平均得分: <strong>%RATINGS\_AVERAGE%</strong>)

下面就是把评分后的文章按着最高评分列表显示出来。

Highest Rated:最高评分列表

<li><a href="%POST\_URL%" title="%POST\_TITLE%">%POST\_TITLE%</a></li>

打分的代码，插入到文章的合适位置。

<span><?php if(function\_exists('the\_ratings')) { the\_ratings(); } ?></span>
