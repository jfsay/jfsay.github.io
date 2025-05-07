---
title: "谷歌发来WordPress的更新提醒"
date: 2012-06-26
categories: 
  - "website"
tags: 
  - "google"
  - "wordpress"
---

邮箱中收到一封主题为“WordPress 有更新”的邮件，心里想着这WordPress也真够蛋疼的，整天在后台提醒不就完了嘛，干嘛还发封邮件来多此一举。

之后却发现发件人的地址是Google的域，原来这是一封谷歌发过来的邮件。内容如下：

> 尊敬的 [http://www.jfsay.com/](https://www.jfsay.com/) 网站所有者或网站站长： 截至最后一次抓取您的网站，您运行的似乎是 WordPress 3.2.1。Google 建议您更新至最新版本。旧版或未安装补丁的软件可能容易遭到黑客或恶意软件的袭击，进而危害您的用户。要下载最新版本，请访问 [WordPress 下载页面](http://wordpress.org/download/)。如果您已更新到 WordPress 的最新版本，请忽略此讯息。 如果您对于收到这条讯息的原因还有其他任何疑问，请查看 Google 关于此主题的[博文](http://googlewebmastercentral.blogspot.com/2009/11/new-software-version-notifications-for.html)，了解更多背景信息。 此致 Google 搜索质量小组敬上

我被上述邮件中的链接引领到['new software version' notifications for you site的博文](http://googlewebmastercentral.blogspot.com/2009/11/new-software-version-notifications-for.html)，文章说谷歌在爬取网站信息时通过分析网页源代码可以找到网站存在的问题，从而通知网站所有者来维护网站。因为WordPress的程序包含meta tag的版本信息，所以谷歌借此来发现你所使用的WordPress的版本问题。

个人感觉WordPress更新太频繁，这些大大小小的更新对使用者来说意义并不是太大，而且总是不提供取消自动保存、自动草稿和版本修订的功能（因为[我为了实现文章的ID连续](http://www.jfsay.com/archives/136.html "WordPress禁用自动保存、自动草稿和修订版本功能（ID连续）")），所以每次WordPress提醒更新时我总是会等待好久，错过它几个版本之后来次大的更新反而省事。

另，因为此博客启用了缓存插件来静态化页面，部分页面没有得到及时的更新，所以谷歌分析的WordPress版本信息可能有误。
