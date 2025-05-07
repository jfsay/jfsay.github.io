---
title: "ChatGTP帮助写.htaccess语句"
date: 2024-12-24
categories: 
  - "software_programming"
tags: 
  - "chatgtp"
---

Google Search Console提醒我有大量网页的「网址不规范」，都是类似这样的网址：https://jfsay.com/page/10?wptouch\_switch=desktop&redirect=%2F%3Fwptouch\_switch%3Ddesktop%26redirect%3D%252Farchives%252F269.html%26nonce%3D45b539a4fe&nonce=91c204e132，看起来是WPtouch跳转的URL，但是我已经卸载WPtouch插件好久了，不知道为什么Google还会访问这样的网址。

之前使用WPtouch插件好多年，它通过浏览器的UA判断是PC端还是移动端，为没有网页自适应的网站提供移动端的网页。后来把WordPress的主题更换成自适应的主题后，就卸载了WPtouch插件。

我首先想到会不会是WPtouch插件没有卸载干净或者有缓存。我花了好长时间，查找了网站的所有文件（将所有文件下载到本地用工具查找），并没有找到WPtouch的相关文件。我又怀疑是数据库有WPtouch的跳转语句，但是也没有找到。

在cPanel面板的「访客」页面，发现每天都有包含wptouch\_switch的URL的访问记录，大部分都是Googlebot产生的。

我在网上找到一个帖子，和我的情况很像，标题是：删除了WPtouch但仍在使用中（Removed WPtouch but still in use）。下面有人回答说可以把网址进行301重定向。我想着这个方法也不错，也打算试下。

我想在.htaccess添加网址301重定向的语句，自己不会写，继续在网上查找，但是网上提供的现成的语句都是简单的，没有正好是我需要的。我试图自己学习RewriteCond和RewriteRule语法，然后自己来写。但是这个语法太难了，实在是看不懂，昨天晚上折腾了两三个小时，还是没有解决。

今天早上突然想到ChatGTP可以帮助写代码，于是试了一下。

我在对话框输入以下内容（请忽略我的塑料英语）：

```
I want to redirect a URL using .htaccess. For example:
From url:https://jfsay.com/page/1?wptouch_switch=desktop&redirect=%2F%3Fwptouch_switch%3Ddesktop%26redirect%3D%252Farchives%252F269.html%26nonce%3D45b539a4fe&nonce=91c204e132 to url:https://jfsay.com/page/1
From url:https://jfsay.com/page/2?wptouch_switch=desktop&redirect=%2F%3Fwptouch_switch%3Ddesktop%26redirect%3D%252Farchives%252F269.html%26nonce%3D45b539a4fe&nonce=91c204e132 to url:https://jfsay.com/page/2
From url:https://jfsay.com/page/80?wptouch_switch=desktop&redirect=%2F%3Fwptouch_switch%3Ddesktop%26redirect%3D%252Farchives%252F269.html%26nonce%3D45b539a4fe&nonce=91c204e132 to url:https://jfsay.com/page/80

I want to redirect a URL using .htaccess. For example:
From url:https://jfsay.com/?wptouch_switch=mobile&redirect=%2Farchives%2F1.html&nonce=30cabb8867 to url:https://www.jfsay.com/archives/1.html
From url:https://jfsay.com/?wptouch_switch=mobile&redirect=%2Farchives%2F2.html&nonce=30cabb8867 to url:https://www.jfsay.com/archives/2.html
From url:https://jfsay.com/?wptouch_switch=mobile&redirect=%2Farchives%2F847.html&nonce=30cabb8867 to url:https://www.jfsay.com/archives/847.html
```

ChatGTP竟然知道我是要批量处理网址的重定向，而且知道哪个是「参数」，它给出了以下的答案。

```
RewriteEngine On
#Redirect for specific pages with the described query string
RewriteCond %{QUERY_STRING} ^wptouch_switch=desktop&redirect=.&nonce=.$ [NC]
RewriteRule ^page/([0-9]+)/?$ /page/$1? [R=301,L]

RewriteEngine On
#Redirect from mobile wptouch with a specific redirect parameter to the archives
RewriteCond %{QUERY_STRING} ^wptouch_switch=mobile&redirect=%2Farchives%2F([0-9]+).html&nonce=[a-zA-Z0-9]+$ [NC]
RewriteRule ^$ https://www.jfsay.com/archives/%1.html? [R=301,L]
```

我把上面的语句粘贴到.htaccess文件里去，试了一下，没想到网址成功跳转了。

ChatGTP太强大了，我昨天花了两三个小时都没有搞定的事情，它几分钟就给解决了。

现在我理解了搜索引擎和ChatGTP的区别了。搜索引擎是「死的」，它通过关键字查找，给出的结果是已经存在的，我们还需要对这些结果进行分析鉴别和后续加工；而ChatGTP是「活的」，可以主动思考，可以产生新的内容。比如我这个需求很难在搜索引擎里描述清楚，从而找到满意的的结果，而ChatGTP可以知道我要进行批量的网址重定向，而且准确地知道哪个是参数，只要你给它举个例子就行。这真的好强大！
