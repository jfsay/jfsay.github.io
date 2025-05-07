---
title: "Feedsky域名绑定方式CNAME"
date: 2010-06-25
categories: 
  - "website"
tags: 
  - "域名"
---

Feedsky的RSS托管服务中的域名绑定现在只支持CNAME，CNAME是什么?CNAME记录是域名名称的别名。

具体的绑定步骤是：

登录到域名的DNS服务器中，解析方式选择CNAME，添加或修改一个子域名，绑定的地址是mydomain.feedsky.com

对于使用Dot TK的免费DNS服务器，CNAME的绑定方式是：

登录→我的域名列表→选择设定的域名→升级→

类型中选择CNAME,主机名中填创建的二级域名（feed.weishanshan.tk），IP地址中填mydomain.feedsky.com
