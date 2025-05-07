---
title: "用HTTPS Everywhere插件解决Flickr图片不能显示问题"
date: 2014-03-06
categories: 
  - "website"
tags: 
  - "flickr"
---

自从[家里装了移动（铁通）的宽带](http://www.jfsay.com/archives/1098.html "慎用中移动（铁通）的宽带网络")以后，最让我蛋疼的是它把Flickr给作死了。我博客的图片全部采用外链自Flickr的形式，这下连自己上传外链图片都不能登录Flickr了。首先想到的[解决办法](http://www.jfsay.com/archives/264.html "解决Flickr部分图片无法显示的问题")是在HOST中添加IP，可是慢慢我发现获得的IP偶尔也会失效，图片依旧不能访问，原来是某些Flickr的整个farm服务器会屏蔽。这时我对自己当初选择外链图片的方式产生了动摇，想着把图片放在自己服务器空间上。

当初图片外链自Flickr也是无奈之举，博客建在免费服务器上，因为服务器不稳定需要[到处搬家](http://www.jfsay.com/archives/420.html "别了，免费空间")，这样只带着数据库数据跑比较方便，而且我们这个属于生活类博客，会有[游记](http://www.jfsay.com/archives/category/travels)之类图片爆多的文章，外链图片不占用服务器空间存储。

外链有外链的好处，也有它的弊端，就是链接失效或者无法访问。图片本来就是个耗资源的大户，没有几家人情愿给你提供免费高效外链的图片服务，国内的类似服务吝啬的要死，选来选去选择了Flickr。

CMCC的网络环境下，虽然Flickr惨不忍睹，但是我发现HTTPS的图片显示却没有问题，但是Flickr的图片默认是没有HTTPS的，于是想找一个能让Flickr图片强制使用HTTPS的方法。然后就让我找到了[HTTPS Everywhere](https://chrome.google.com/webstore/search-extensions/https%20everywhere)这个Chrome插件。装上该插件以后，Flickr的图片又活了过来，再也不用笨手笨脚地去添加IP了，而且Flcikr的farm服务器也在不断增加，这样我总算可以在自己的电脑上使用Flickr了。

说实在的，在当下国内的网络环境，有HTTPS总比没有好，能用HTTPS就尽量用吧，虽然它会影响你丁点儿网速，但对你我来说必定是利大于弊的。
