---
title: "WordPress空间转移到Godaddy免费空间的过程小结"
date: 2012-10-16
categories: 
  - "website"
tags: 
  - "mysql"
  - "wordpress"
  - "数据库"
  - "空间"
---

自从Godaddy的免费空间没有广告以后，我就试图[换用Godaddy的免费空间](http://www.jfsay.com/archives/644.html)，现在把空间迁移的过程小结一下。

#### 1、安装WordPress程序

问题：直接安装WordPress失败

Godaddy的空间控制面板中存在直接安装WordPress程序的链接，但是直接点击却无法安装，据说是免费空间不提供此功能。

解决：手动安装

通过FTP上传WordPress程序压缩包，然后解压缩即可。

#### 2、MySQL数据库转移

**问题1：数据库无法成功转移**

通过phpMyadmin备份数据库，然后通过phpMyadmin恢复数据库，出现错误，提示信息为“#1062 – Duplicate entry ’2′ for key 1 Duplicate entry ‘%s’ for key %d 错误编号：1062”

尝试：不通过phpMyadmin来恢复数据库，而是通过Godaddy空间的MySQL数据库自带的数据库还原功能。具体步骤是：

> 1、通过FTP将数据库备份文件上传到godaddy主机根目录下的\_db\_backups目录内（如果\_db\_backups目录不存在，就手工创建），数据库备份文件后缀需为.sql（如果是.txt需要改为.sql）。
> 
> 2、进入主机管理面板Host control center后，点击菜单Databases，然后点击子菜单MySQL，进入MySQL数据库管理界面。
> 
> 3、点击要导入的数据库后面的小铅笔符号（此符号为数据库编辑图标）。
> 
> 4、点击小铅笔符号后进入MySQL数据库编辑界面，然后点击菜单Restore。
> 
> 5、点击Restore后展开一个界面。这个界面里列出主机根目录下\_db\_backups目录里的.sql文件。选择要恢复的.sql文件，或者要导入的.sql文件，然后点击橙色Restore按钮。这样系统就开始将选中的.sql文件中的数据导入到MySQL数据库中了。

不过我通过以上步骤来试图恢复数据库，几次尝试都没有成功，作罢。

解决：通过WordPress备份插件WordPress Database Backup来备份数据库

出现数据库无法成功转移的原因是mysql数据库版本不同而导致Wordpress数据库导入出错，我通过此插件重新备份数据库，然后通过phpMyadmin恢复数据库，结果成功了。但是出现了下面一个问题。

**问题2：文章正文出现乱码，显示的是一连串的问号“?”**

明眼人一看便知这是数据库编码的问题，由于两个数据库编码不同而产生数据库的内容乱码了。

我开始尝试通过phpMyadmin来反复修改数据库的编码，比如latin1和utf8等。可是不管我把数据库的编码修改成什么类型，最终还是不能解决问题。

解决：通过cosdbrecover.php 方案

通过江东大哥的“[WordPress数据库转移乱码解决方案](http://www.storyday.com/html/y2007/911_wordpress-i18n-solution.html)”来恢复数据库，结果是出现了下一个问题。

**问题3：问号变成了乱码**

虽然问题还没有解决，但是我知道已经前进了一大步，因为这一堆乱码和源数据库中的乱码是一致的。

解决：WordPress数据库导入乱码

修改WordPress根目录下的confing.php配置文件，进行如下修改（就是去掉utf8）：

define('DB\_CHARSET', 'utf8');  →  define('DB\_CHARSET','');

话外：在我尝试通过传说中的“帝国备份”来恢复数据库时，Godaddy的FTP File Manager出现了问题，显示" Cannot find home. Please try again in a few minutes. If the problem persists, please contact support." 或者 "Could not get directory info." 提示。

在我向Godaddy提交维修单之后问题得到解决。
