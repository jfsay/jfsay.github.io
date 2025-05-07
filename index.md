---
layout: default  # 使用一个布局文件（可选）
title: Home     # 页面标题
---
# 最新文章

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}