---
title: "终于解决了WordPress手机端发布文章的问题——都是XMLRPC惹的祸"
date: 2022-11-21
categories: 
  - "website"
tags: 
  - "wordpress"
  - "xmlrpc"
---

现在博客里的绝大多数文章都是在手机上写的，写好以后也是通过手机来发布。

今年[7月开始](https://www.jfsay.com/archives/1986.html)，WordPress手机客户端发布文章的时候总是提示失败，怎么都弄不好，于是把这个APP卸载了，重新安装，重新绑定站点，这时提示「无法连接。服务器上没有所需的XML-RPC方法」。

这时我知道问题出现在xmlrpc上了，我反复找主机商好几次，主机商说他什么都没有做，让我自己停用所有的插件和使用默认主题试一下，我尝试之后问题还是没有解决。

我之后在网上查找「xmlrpc不能使用」的原因，没想到找到的却是「xmlrpc禁用」的方法，心想禁用的方法反过来也就是使用的方法，于是我把这些禁用xmlrpc的方法都看了一遍。方法有如下几个：修改functions.php、.htaccess文件、wp-config.php、Apache配置文件和安装插件等。除了Apache配置文件因为没有权限查看和修改外，其他的我都试了还是没有解决。

我把整个站点的文件下载了下来，使用查找文件内容的软件来搜索「xmlrpc」和「xml」的关键字，一个个文件来查找，没有找到问题所在。

后来发现访问https://jingfengshuo.com/xmlrpc.php会跳转到127.0.0.1，于是又去搜索WordPress做301重定向的方法，想看下哪里做了这个重定向，找了cpanel和.htaccess也没找到xmlrpc.php被跳转的地方。

实在找不到解决办法，就去WordPress的官方论坛看看，看来看去也没找到同样问题的帖子。

试了好多方法都没能解决，只好作罢，我在手机浏览器里收藏了博客的后台网址，这几个月只能通过手机浏览器用账号密码登录后台来发布文章，虽然不方便但也能用。

今天在博客后台搜索xmlrpc的插件，发现一款名叫「Rename XMLRPC」的插件，它的介绍如下：

> Make XML-RPC work if you rename the file. Some hosts block access to xmlrpc.php file making it impossible to use

这不就是我要的功能吗？真的是踏破铁鞋无觅处啊。我赶紧安装了这个插件，安装后却没找到配置和使用界面，再打开插件的详情页面，作者写的几句话的使用方法实在看不懂。于是打开插件文件来看代码，看到作者使用xmlrpc2.php这个名字。于是我把自带的xmlrpc.php复制了一份，重命名为xmlrpc2.php，然后再WordPress安卓客户端绑定网站，输入https://www.jfsay.com/xmlrpc2.php，成功绑定了网站！

时隔四个月，终于又能在WordPress手机客户端连接网站了，这四个多月我花了几十个小时来解决这个问题而不得，现在总算解决了，太高兴了！
