---
title: "WordPress备份的内容及方法"
date: 2025-03-05
categories: 
  - "website"
tags: 
  - "wordpress"
  - "备份"
---

为了防止意外发生，需要定期备份WordPress的数据，以下是我根据自己的需要整理的备份内容及方法：

## 1\. **备份数据库**

- **使用插件**：如Database Backup for WordPress插件，可自动备份数据库到电子邮箱。（**频率**：每周一次，自动）

- **数据库操作**：通过phpMyAdmin导出数据库文件。（**频率**：每年一次，手动）

## 2\. **备份文章**

- **备份到博客托管平台**：WordPress后台导出xml文件，然后导入到WordPress.com或者Blogger。（**频率**：每年一次，手动）

- **电子邮件备份**：使用电子邮件订阅博客服务（如follow.it），每次更新文章时，将会收到邮件。（**频率**：每次发布文章一次，自动）

## 3\. **备份文件**

- **主题文件**：备份`wp-content/themes`目录。

- **wp-config.php**：包含数据库连接信息等重要配置。

- **.htaccess**：用于URL重写等服务器配置。

- **robots.txt**：搜索引擎规则。

- **favicon.ico**：网站图标。

- **上传文件**：备份`wp-content/uploads`目录。因为我的图片全部是外链，不需要备份这个文件夹。

- **手动备份**：通过FTP或文件管理器下载文件。

- **频率**：每次修改后立即备份。

## 4\. **备份外链图片**

- **查找包含图片的文章**：  
    `SELECT ID, post_title,guid FROM wp_posts WHERE post_type = 'post' AND post_content LIKE '%<img%';`

- **查找包含2张及以上图片的文章**：  
    `SELECT ID, post_title, guid FROM wp_posts WHERE post_type = 'post' AND (LENGTH(post_content) - LENGTH(REPLACE(post_content, '<img', ''))) / LENGTH('<img') >= 2;`

- **备份方法**：手动将文章复制粘贴到国内各大平台，如微信号、知乎、豆瓣、头条号等，这些平台会自动将外链图片上传到自身的服务器。

- **频率**：不定期备份。
