---
title: "同一主机空间更换域名并进行301跳转的步骤"
date: 2015-05-06
categories: 
  - "website"
tags: 
  - "wordpress"
  - "域名"
---

这次更换域名比想象地快了很多，我预计要一两天的时间才能把域名更换工作做完，实际上比想象中简单地多，顺利地话也就一两个小时就能完成了。下面记录一下更换域名的步骤。

**0、 前提条件**

因为是更换域名，也就是你现在已经拥有了一个可以正常访问的旧域名，比如jingfeng.info。而且有一个主机空间，我这里是Linux的虚拟主机，分配的IP地址是173.201.216.17。

**1、 注册新域名**

以前的域名是Godaddy上注册的，用了4年了，Godaddy有一个非常恶心人的做法是头年便宜，吸引你过去，之后每年的续费很贵。这次注册新域名选择了namesilo，价格公道又实惠，没有隐形消费，还送永久的隐私保护，每年都是8.99$，用过优惠码后是7.99$，算起来比Godaddy划算。顺便推荐个[域名优惠码的网站](https://www.domcomp.com/?refcode=550a16c212000027034725ca)，更新很频繁。

另外，namesilo现在支持支付宝的付款方式，大大方便了国内用户购买。

**2、 旧主机空间绑定新域名**

我在namesilo上注册了新域名jingfengshuo.com，下一步就是在Linux的虚拟主机上绑定这个域名。

登录主机的管理界面（各主机的管理界面不一样），在“hosted domain”或者“Park domain”中添加新域名jingfengshuo.com。

**3、 新域名修改A记录指向主机IP地址**

登录域名的DNS Server管理界面，添加一条A记录，如下：

A    173.201.216.17     3600

等待DNS解析生效。我这里使用的是namesilo自带的DNS解析服务，话说namesilo域名解析生效的时间可真长啊，等了我一两个小时才生效。

可以使用PING命令检测域名解析是否生效，在CMD的命令行窗口中ping的新域名，比如：ping jingfengshuo.com –t

如果返回的IP地址为173.201.216.17则说明域名解析已经生效，指向了正确的IP地址上了。

**4、 全站进行301重定向**

301跳转能把旧域名的遗产交给新域名，告诉搜索引擎新域名是合法的继承者。我这边中午做过旧域名的301跳转，晚上在谷歌和百度上发现新域名已经被收录了十几个页面了。Linux进行301重定向异常简单，只需在网站根目录下的.htaccess添加如下语句：

```
RewriteEngine On
RewriteCond %{HTTP_HOST} ^jingfeng.info [OR]
RewriteCond %{HTTP_HOST} ^www.jingfeng.info [NC]
RewriteRule ^(.*)$ http://www.jingfengshuo.com/$1 [L,R=301]
```

**5、 修改网站和数据库中旧域名的地址**

经过上一步操作，旧域名已经能跳转至新域名了，下面就是把旧域名下的网站中的内容修改为新域名的地址。下面的3条语句针对WordPress数据库进行替换操作，分别是修改WordPress设置、文章内容、文章链接中的域名超链接地址。

具体方法是：在 phpMyAdmin 中点击 “SQL”，输入以下代码，然后执行。

```
UPDATE wp_options SET option_value = REPLACE( option_value, ' http://www.jingfeng.info', ' http://www.jingfengshuo.com ' ) WHERE option_name = 'home' OR option_name ='siteurl' ;
UPDATE wp_posts SET post_content = REPLACE( post_content, 'http://www.jingfeng.info' , 'http://www.jingfengshuo.com' ) ;
UPDATE wp_posts SET guid = REPLACE( guid, 'http://www.jingfeng.info' , 'http://www.jingfengshuo.com' ) ;
```

**6、谷歌站长工具、百度站长工具做域名的更换操作**

以上步骤完成后，新域名的更改工作也就做完了，可以额外做一个优化工作，就是在Google网站站长工具和百度站长平台中做域名的更换操作，告诉谷歌和百度网站地址由旧域名指向新域名。该操作能加快谷歌和百度对新域名收录速度，有益于SEO。
