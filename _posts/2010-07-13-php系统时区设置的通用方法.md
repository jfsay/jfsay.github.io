---
title: "PHP系统时区设置的通用方法"
date: 2010-07-13
categories: 
  - "website"
tags: 
  - "php"
---

我使用的服务器空间是ATBhost，网站有些文件需要调用系统时间，发现系统时间和需要的北京时间总是相差12个小时，一直在寻找设置时区的地方。开始以为在ATBhost的Contrl panel里面设置，找来找去找不到设置时区的选项；之后在cPanel里寻找，还是同样没有找到；网上有人说可以设置mysql数据库的时区，最终发现没有权限修改。功夫不负有心人，设定时区终于给解决了。下面介绍系统时间和北京时间相差的两种解决方法：

方法一：

在public\_html中找到php.ini,没有的话可以自己新建一个同名的文件，然后上传到此文件夹中。

php.ini中有“;date.timezone”这么一项，它是用来设置时区的，默认状态下是关闭的，我们需要开启它。如果需要的是上海时间，那么就设置成：date.timezone = "Asia/Shanghai"。其他可用的值是：Asia/Chongqing 、Asia/Shanghai 、Asia/Urumqi （依次为重庆，上海，乌鲁木齐）；港台地区可用：Asia/Macao、Asia/Hong\_Kong、Asia/Taipei（依次为澳门，香港，台北）；还有新加坡：Asia/Singapore；以及：Etc/GMT-8、Singapore、Hongkong、PRC.

方法二：

在需要修改时区的PHP文件中使用date\_default\_timezone\_set('Asia/Shanghai');然后再使用date函数$time = date(Y."年".m."月".d."日".G."时".i."分");调用就行了。
