---
title: "Robots文件设置示例"
date: 2010-06-13
categories: 
  - "website"
tags: 
  - "php"
  - "robots"
---

Robots使得网络蜘蛛按规矩搜索网站，也可以使蜘蛛远离某些服务器上的目录。下面是一个Robots.txt的例子：

User-agent: \*  
Disallow: /admin/   后台管理文件  
Disallow: /require/   程序文件  
Disallow: /attachment/  附件  
Disallow: /images/     图片  
Disallow: /data/       数据库文件  
Disallow: /template/   模板文件  
Disallow: /css/       样式表文件  
Disallow: /lang/      编码文件  
Disallow: /script/    脚本文件

\*表示对于所有的搜索引擎，Disallow表示不允许访问的目录，如果网站建有站点地图，只需在Robots.txt中添加下列行：

Sitemap: http://www.example.com/**sitemap.xml**
