---
title: "分页插件WP-PageNavi的后台设置"
date: 2011-05-16
categories: 
  - "website"
tags: 
  - "wordpress"
  - "插件"
---

WordPress精简到连分页导航的功能也不提供了，本人使用的是WP-PageNavi分页插件，该插件使用也很简单，安装之后需要到后台进行相应的（个性化）设置。

下面是WP-PageNavi的设置选项：

**1****、“页数”文字设置（****Text For Number Of Pages****）**

该选项显示的是总共的页数和当前的页码，可设置为：共%TOTAL\_PAGES%页 第%CURRENT\_PAGE%页，显示的效果是：共30页 第7页

**2****、“当前页数”文字设置（****Text For Current Page****）**

显示的当前的页数（如：3），可设置为：%PAGE\_NUMBER%

**3****、“页数”文字设置（****Text For Page****）**

显示的是页数的格式（如：1 2 3），可设置为：%PAGE\_NUMBER%

**4****、“首页”文字设置** **（****Text For First Post****）**

显示的是最前一页（首页）的格式，可设置为：&laquo最前，显示的效果是：« 最前

**5****、“尾页”文字设置** **（****Text For Last Post****）**

显示的是最后一页（尾页）的格式，可设置为：&raquo最后，显示的效果是：最后 »

**6****、“下一页”文字设置（****Text For Next Post** **）**

显示的是下一页的格式，可设置为：&raquo，显示的效果是：»

**7****、“上一页”文字设置（****Text For Previous Post****）**

显示的是上一页的格式，可设置为：&laquo，显示的效果是：«

**8****、“下一页”省略文字设置（****Text For Next …****）**

显示的是下一页格式，可设置为：…,显示的效果是：…

**9****、上一页”省略文字设置（****Text For Previous …****）**

显示的是上一页格式，可设置为：…,显示的效果是：…

**通过以上设置，最终显示的效果是：**

共29页 第6页[« 最前](https://www.jfsay.com/)...[«](http://www.jfsay.com/page/5) [3](http://www.jfsay.com/page/3) [4](http://www.jfsay.com/page/4) [5](http://www.jfsay.com/page/5) **6** [7](http://www.jfsay.com/page/7) [8](http://www.jfsay.com/page/8) [9](http://www.jfsay.com/page/9) [»](http://www.jfsay.com/page/7)...[最后 »](http://www.jfsay.com/page/29)

**10****、使用pagenavi- css.css**

是否使用插件自带的CSS文件。

**11****、总是显示页面导航，即使只有一个网页也显示导航。（****Always Show Page Navigation** **）**

**12****、显示多少页数**

显示的页数为多少，若设置为7，则显示的效果是1 2 3 4 5 6 7共七个页码。

**13****、显示较大页面页数**

是否显示较大的页面数，设置为0，表示禁用此功能。若设置为2，则显示两个较大页面。这个选项需要和下一个选项配合使用，若禁用则下一个也同时被禁用了。

**14****、大页面页数的显示倍数：**

该选项是较大页面的相隔倍数，需要和上一个选项配合使用。

若这里设置为10，上一项设置为2，则显示的效果是：共29页 第1页 **1** [2](http://www.jfsay.com/page/2) [3](http://www.jfsay.com/page/3) [4](http://www.jfsay.com/page/4) [5](http://www.jfsay.com/page/5) [6](http://www.jfsay.com/page/6) [7](http://www.jfsay.com/page/7) [»](http://www.jfsay.com/page/2) [10](http://www.jfsay.com/page/10) [20](http://www.jfsay.com/page/20)...[最后 »](http://www.jfsay.com/page/29)

这里显示的是2个较大页面（10和20），它们之间的倍数是10.
