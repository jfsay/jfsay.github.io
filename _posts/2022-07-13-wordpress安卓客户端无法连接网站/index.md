---
title: "WordPress安卓客户端无法连接网站"
date: 2022-07-13
categories: 
  - "website"
tags: 
  - "wordpress"
  - "xmlrpc"
---

前几天用安卓手机的WordPress APP发布文章的时候老是提示失败，也不知道是什么原因。我把WordPress APP绑定的站点给删除了，重新绑定网站的时候提示「无法连接。服务器上没有所需的XML-RPC方法。」

上网搜了一下，有人说是由于主机商禁用了XML-RPC导致的。

于是联系主机服务商：「 请问主机是否禁用了XML-RPC？」主机商说没有。

我只能自己排查。突然想到微软有一款live write 的软件可以写博客。我装了以后在绑定网站的时候提示https://jingfengshuo.com/xmlrpc.php永久重定向。

然后发现xmlrpc.php被做了301的重定向，访问https://jingfengshuo.com/xmlrpc.php时候会跳转到127.0.0.1，这时我才明白为什么WordPress找不到xmlrpc方法了，本来就不存在肯定就找到了。

于是我排查怎么做了重定向？先去.htaccess看下，没找到。又打开xmlrpc.php文件，看了也是没有。登录WordPress后台看插件和主题，还是没有。最后找cPanel，也没有找到。

这下我就纳闷了，我把xmlrpc.php删除掉，还是会301重定向，看来是服务器层做的了。我又去问了主机商，主机商答复还是没有。

找来找去确实找不到原因了，又想在手机上登录WordPress来发布文章，只能用手机浏览器登录后台了。

**更新（已解决）**

确认问题出现在xmlrpc上，但是又不知道哪里做了限制，导致xmlrpc.php无法使用。解决方法可查看以下文章：[终于解决了WordPress手机端发布文章的问题——都是XMLRPC惹的祸](https://www.jfsay.com/archives/2224.html)
