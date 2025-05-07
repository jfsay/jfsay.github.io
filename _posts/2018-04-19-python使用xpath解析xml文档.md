---
title: "Python使用XPath解析XML文档"
date: 2018-04-19
categories: 
  - "software_programming"
tags: 
  - "python"
---

XPath（XML Path Language）是一种小型的查询语言：

1）可在XML中查找信息

2）支持HTML的查找

3）通过元素和属性进行导航

python开发使用XPath条件：

由于XPath属于lxml库模块，所以首先要安装库lxml

XPath的使用方法：

首先讲一下XPath的基本语法知识：

四种标签的使用方法

1) **//** 双斜杠 定位根节点，会对全文进行扫描，在文档中选取所有符合条件的内容，以列表的形式返回。

2) **/** 单斜杠 寻找当前标签路径的下一层路径标签或者对当前路标签内容进行操作。

3) /text() 获取当前路径下的文本内容。

4) /@xxxx 提取当前路径下标签的属性值

5) **|** 可选符 使用|可选取若干个路径 如//p | //div 即在当前路径下选取所有符合条件的p标签和div标签

6) **.** 点 用来选取当前节点

7) .. 双点 选取当前节点的父节点

_注：以下代码在Python3.6.1下调试通过_

一、Python读取XML简单实例

```
from lxml import etree
text = """
<data>
    <country name="Liechtenstein">
        <rank>1</rank>
        <year>2008</year>
        <gdppc>141100</gdppc>
        <neighbor name="Austria" direction="E"/>
        <neighbor name="Switzerland" direction="W"/>
    </country>
    <country name="Singapore">
        <rank>4</rank>
        <year>2011</year>
        <gdppc>59900</gdppc>
        <neighbor name="Malaysia" direction="N"/>
    </country>
    <country name="Panama">
        <rank>68</rank>
        <year>2011</year>
        <gdppc>13600</gdppc>
        <neighbor name="Costa Rica" direction="W"/>
        <neighbor name="Colombia" direction="E"/>
    </country>
</data>
"""

root = etree.XML(text)
for child in root:
   print(child.tag, child.attrib)
   print('rank',child.xpath('./rank/text()')[0])
   print('year', child.xpath('./year/text()')[0])
   print('gdppc', child.xpath('./gdppc/text()')[0])
   print('neighbor', child.xpath('./neighbor/@name')[0])
```

二、Python读取本地XML简单实例

如果XML文档存放在本地，可以文件对象打开xml就读取成字符串类型，也可以直接tree = etree.parse("D:/lujing/test.xml")读取。

```
etree.parse("D:/lujing/test.xml")
from lxml import etree
tree = etree.parse("D:/lujing/test.xml")
root = tree.getroot()

for child in root:
   print(child.tag, child.attrib)
   print('rank',child.xpath('./rank/text()')[0])
   print('year', child.xpath('./year/text()')[0])
   print('gdppc', child.xpath('./gdppc/text()')[0])
   print('neighbor', child.xpath('./neighbor/@name')[0])
```

三、为防止读取XML出错导致程序退出，可使用try捕获异样

```
from lxml import etree
tree = etree.parse("D:/lujing/test.xml")
root = tree.getroot()

root = etree.XML(text)
for child in root:
   try:
       print(child.tag, child.attrib)
       print('rank',child.xpath('./rank/text()')[0])
       print('year', child.xpath('./year/text()')[0])
       print('gdppc', child.xpath('./gdppc/text()')[0])
       print('neighbor', child.xpath('./neighbor/@name')[0])
       print('neighbor', child.xpath('./neighbor/@name')[1])
   except Exception as e:
        print(e)
```
