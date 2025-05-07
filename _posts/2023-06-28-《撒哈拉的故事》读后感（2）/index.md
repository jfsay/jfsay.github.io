---
title: "WordPress设置robots.txt的最佳方法"
date: 2023-06-28
categories: 
  - "website"
tags: 
  - "robots"
  - "seo"
  - "wordpress"
---

很久以前我就设置了博客的robots.txt，想让搜索引擎只抓取网站中关键的内容，不抓取后台的文件和页面。这样做的原因如下：

> 搜索机器人对每个网站都有一个爬网配额，这意味着它们在爬网会话期间对一定数量的网页进行爬网。如果他们没有完成对您网站上所有网页的抓取，那么它们将在下一个会话中返回并恢复抓取。这可能会减慢网站索引的速度。
> 
> 您可以通过禁止搜索机器人尝试抓取不必要的页面（如 WordPress 管理页面、插件文件和主题文件夹）来解决此问题。通过禁止不必要的网页，可以节省搜索引擎爬网配额。这有助于搜索引擎抓取网站上的更多页面并尽快将其编入索引。

我在网上各处寻找robots.txt的设置方法，取各家之长最终将robots.txt设置如下（**注意现在这个方法已经过时了**）：

```
User-agent: *

Disallow: /wp-admin/

Disallow: /wp-content/

Disallow: /wp-includes/

Disallow: /trackback/

Disallow: /comments/

Disallow: /attachment/

Disallow: /comments/feed

Disallow: /feed

Disallow: /*/feed

Disallow: /*/comment-page-*

Disallow: /*?replytocom=*

Disallow: /*/trackback

Disallow: /?s=*

Disallow: /*/?s=*\

Disallow: /wp-*.php
```

最近我才知道这样设置robots.txt已经是不对的（过时了），因为搜索引擎在不断进步，上面那样设置robots.txt反而不利于搜索引擎索引。而且即使一个页面被robots.txt阻止了，它可能仍会被编入索引，如果不想让它被搜索引擎索引，最好的方法是在页面上放置noindex元标记。

因为WordPress已经自动阻止索引某些敏感文件和URL，例如WordPress管理区域，所以，对于WordPress，设置robots.txt最好的示例如下（对于所有爬虫程序不受限制地自由抓取这个网站）：

```
User-Agent: *

Disallow:

Sitemap: https://www.example.com/sitemap_index.xml
```

**以下内容来源自：https://yoast.com/ultimate-guide-robots-txt/**

**robots.txt优点：管理爬网预算**

通常可以理解，搜索蜘蛛到达一个网站时，会预先确定它将抓取多少页面（或它将花费多少资源/时间，基于网站的权威/大小/声誉，以及服务器的响应效率）。SEO称之为爬行预算。

如果您认为您的网站存在抓取预算问题，阻止搜索引擎将精力「浪费」在网站的不重要部分可能意味着专注于重要的部分。

有时阻止搜索引擎抓取您网站有问题的部分可能是有益的，尤其是在必须进行大量 SEO 清理的网站上。整理好东西后，您可以让它们重新进入。

**robots.txt缺点：不从搜索结果中删除页面**

即使您可以使用robots.txt文件告诉爬虫它不能在您的网站上的位置，您也不能使用它向搜索引擎说哪些URL不会显示在搜索结果中。换句话说，阻止它不会阻止它被索引。如果搜索引擎找到足够的指向该 URL 的链接，它将包含它；它只是不知道该页面上的内容。

如果您想可靠地阻止网页出现在搜索结果中，请使用noindex元标记。这意味着要找到该标记，搜索引擎必须能够访问该页面，因此不要用robots.txt阻止它。 

**使用 noindex 阻止搜索引擎编入索引**（https://developers.google.cn/search/docs/crawling-indexing/block-indexing?hl=zh-cn）

noindex 是一个包含 <meta> 标记或 HTTP 响应标头的规则集，用于防止支持 noindex 规则的搜索引擎（例如 Google）将内容编入索引。当 Googlebot 抓取该网页并发现该标记或标头时，Google 就会完全阻止该网页出现在 Google 搜索结果中，不论是否有其他网站链接到该网页。

**不要在robots.txt中阻止CSS和JS文件**

自2015年以来，Google Search Console警告网站所有者不要阻止CSS和JS文件。多年来，我们一直告诉你同样的事情：不要在你的robots.txt中阻止CSS和JS文件。让我们解释一下为什么您不应该阻止Googlebot的这些特定文件。

通过阻止CSS和JavaScript文件，您可以阻止Google检查您的网站是否正常运行。如果您屏蔽了文件中的 CSS 和 JavaScript 文件，Google 将无法按预期呈现您的网站。现在，谷歌无法理解您的网站，这可能会导致排名降低。此外，甚至像 Ahrefs 这样的工具也会渲染网页并执行 JavaScript。所以，如果你想让你最喜欢的SEO工具工作，不要阻止JavaScript。

这与谷歌变得更加「人性化」的普遍假设完全一致。谷歌希望像人类访问者一样查看您的网站，以便它可以区分主要元素和附加元素。谷歌想知道JavaScript是增强了用户体验还是破坏了用户体验。

**robots.txt缺点：不传播链接值**

如果搜索引擎无法抓取网页，则无法将链接值分布在该网页上的链接中。当你在robots.txt中阻止了一个页面时，这是一个死胡同。任何可能流向（和流经）该页面的链接值都将丢失。

传统上，WordPress喜欢阻止对wp-admin和wp-include目录的访问。 但是，这已经不再被视为最佳实践。

**以下内容来源自：https://kinsta.com/blog/wordpress-robots-txt/#what-to-put-in-your-robotstxt-file**

robots.txt并不是控制搜索引擎索引哪些页面的万无一失的方法。如果您的主要目标是阻止某些页面包含在搜索引擎结果中，正确的方法是使用noindex元标记或密码保护。

这是因为你的robots.txt并没有直接告诉搜索引擎不要索引内容——它只是告诉他们不要抓取它。虽然 Google 不会从您的网站内部抓取标记区域，谷歌自己声明如果外部网站链接到您使用 robots.txt 文件排除的网页，Google 仍可能会将该网页编入索引。

谷歌网站管理员分析师约翰·穆勒（John Mueller）也证实，如果一个页面有指向它的链接，即使它被 robots.txt阻止了，可能仍会被编入索引。

**以下内容来源自：https://yoast.com/wordpress-robots-txt-example/**

搜索引擎不断改进他们抓取网络和索引内容的方式。这意味着几年前曾经是最佳实践的东西可能不再有效，甚至可能损害您的网站。

如今，最佳实践意味着尽可能少地依赖robots.txt文件。只有当您遇到复杂的技术挑战（例如，具有分面导航的大型电子商务网站）或没有其他选择时，才真正需要robots.txt文件中的URL。

通过robots.txt阻止URL是一种“蛮力”方法，可能会导致比解决更多的问题。

对于大多数WordPress网站，以下示例是最佳实践：

```
User-Agent: *

Disallow:

Sitemap: https://www.example.com/sitemap_index.xml
```

这段代码有什么作用？

1. User-agent: \* 该指令指出，以下任何说明适用于所有爬网程序。

3. Disallow: 该指令没有进一步的说明，所以我们说，所有爬虫都可以不受限制地自由抓取这个网站。

5. 在robots.txt文件中，我们还链接到XML站点地图的位置，使Google，Bing和其他搜索引擎更容易找到它。

7. 我们还为查看文件的人提供了一些信息（链接到此页面），以便他们了解我们为什么以这种方式设置文件。

WordPress和Yoast SEO已经自动阻止索引某些敏感文件和URL，例如WordPress管理区域（通过x-robots HTTP标头）。

**robots.txt创造死胡同**

搜索引擎需要发现、抓取和索引您的页面，然后您才能在搜索结果中争夺可见性。如果您通过 robots.txt 阻止了特定网址，搜索引擎将无法再抓取这些页面以发现其他网址。这可能意味着关键页面不会被发现。

**robots.txt否认其价值**

SEO的基本规则之一是来自其他页面的链接会影响您的表现。如果某个网址被阻止，搜索引擎不仅不会抓取它，而且还可能不会分发指向该网址或通过该网址_到_网站上其他页面的任何“链接值”。

**谷歌完全呈现您的网站**

人们过去常常阻止对CSS和JavaScript文件的访问，以使搜索引擎专注于那些最重要的内容页面。如今，谷歌获取你所有的样式和JavaScript，并完全呈现你的页面。了解页面的布局和呈现方式是评估质量的关键部分。所以谷歌不喜欢你拒绝它访问你的CSS或JavaScript文件。

以前阻止访问您的目录和插件目录的最佳实践不再有效，这就是为什么我们与 WordPress 合作删除了 4.0 版的默认禁止规则。

**链接到您的 XML 站点地图有助于发现**

robots.txt 标准支持将指向 XML 站点地图的链接添加到文件中。这有助于搜索引擎发现您网站的位置和内容。

这可能感觉是多余的，因为您应该已经将站点地图添加到Google Search Console和Bing网站管理员工具帐户中，以访问分析和性能数据。但是，在robots.txt 中拥有该链接为爬虫提供了一种万无一失的方式来发现您的站点地图。
