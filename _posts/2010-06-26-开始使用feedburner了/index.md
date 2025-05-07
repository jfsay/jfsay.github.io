---
title: "Feedburner的域名绑定和添加国产订阅器"
date: 2010-06-26
categories: 
  - "website"
tags: 
  - "feedburner"
---

抛弃Feedsky开始使用Feedburner了。Feedburner可以帮你烧制feed、提供永久地址，让你无论换多少次bsp都不用为feed地址变了而烦心。这样的话，你就可以把feed交给Feedburner来管理了。

由于现在还没有支持中文，研究了好长时间才把网站的Feed订阅搞好（前一段时间上线了简体和繁体中文，由于翻译质量不理想下线了）。

因为Feedburner的域名绑定服务在国内被封，绑定域名时，在添加cname记录时不是Feedburner提供的那个cname地址，需要修改为 google.dns.tancee.com这样就行了。和Feedsky不一样，比如说绑定feed.xxx.com，得到的订阅地址是feed.xxx.com/xxx。

在Feedburner中添加国产的订阅器的具体操作是：登录→Optimize→BrowserFriendly→在Appearance Options中选择More subscription options→在输入框中输入如下地址，点击Add即可。

1. 鲜果：http://tools.orzdream.com/RSS-Feed/fb-xg.xml
2. 抓虾：http://tools.orzdream.com/RSS-Feed/fb-zx.xml
3. QQ：http://tools.orzdream.com/RSS-Feed/fb-qq.xml
4. 九点：http://tools.orzdream.com/RSS-Feed/fb-jd.xml
5. 有道：http://tools.orzdream.com/RSS-Feed/fb-yd.xml
