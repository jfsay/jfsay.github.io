---
title: "Python使用xpath解析带命名空间的XML"
date: 2018-05-08
categories: 
  - "software_programming"
tags: 
  - "python"
---

xpath解析XML简单明了，但是XML有命名空间的话就会出错了。解决方法是节点前加命名空间的前缀，下例中x、y是变量可以任意定义。

例如XML文档如下：

```
<a xmlns:a="http://www.jfsay.com" xmlns:b="http://jingfengshuo.com">
    <b>Text</b>
<a>
```

解析代码片段：

```
tree = etree.parse(path)
        root = tree.getroot()        
        for child in root:
             r=child.xpath('x:a/y:b/text()',namespaces={'x': 'www.jingfengshuo.com',
               'y': 'jingfengshuo.com'})[0] 
```

如果XML文档如下：

```
<a xmlns:="http://www.jfsay.com">
    <b>Text</b>
<a>
```

解析代码片段：

```
tree = etree.parse(path)
        root = tree.getroot()        
        for child in root:
             r=child.xpath('x:a/x:b/text()',namespaces={'x': 'www.jingfengshuo.com'})[0]
```
