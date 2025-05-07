---
title: "ghs.google.com是什么？"
date: 2011-01-11
categories: 
  - "software_programming"
tags: 
  - "feedburner"
  - "ghs"
---

Google Blogger、Google Apps企业应用套件、谷歌旗下的FeedBurner，这些服务会提供一个默认的地址A用来访问，但是用户有使用自定义的地址B来访问上述服务的诉求，这里就要使用ghs.google.com了。方法是，自定义一个域名B，然后设置该域名的Cname到ghs.google.com就可以了。

但是现在这个方法不顶用了，因为ghs.google.com被墙了。解决的方法之一是，把要自定义的域名地址B做A记录到一个没有被墙的ghs.google.com的IP. 之二是，先把任意一个域名C做A记录到一个没有被墙的ghs.google.com的IP，然后再把自定义域名B做CNAME到该域名C.

简单的图示为：

- 方法一是：B→IP
- 方法二是：B→C→IP

方法二的好处是显而易见的，当C对应的IP被封的话，只需修改C的A记录到一个新的可用IP即可，C上面所附着的B、D、E等等都可以不用修改，比较方便。

这里面提到的域名C，自己可以随意定义，也可以使用网络上共享的地址，比如google.dns.tancee.com

区别是当域名C所指向的IP被墙之后，自己定义的地址C要自己去更新A记录指向，使用别人的地址C要别人去更新。一般选用使用人数比较多的镜像，因为比较多人用的话，ghs镜像的域名所有者就会有点服务意识，当IP被封的话，可以及时更改镜像的A记录指向。不过就目前来看，ghs.google.com可用的IP已经很少了。

相关阅读：

1. http://blog.linggan.com/google-app-ghs-gfw.html
2. http://blog.tancee.com/ghs
