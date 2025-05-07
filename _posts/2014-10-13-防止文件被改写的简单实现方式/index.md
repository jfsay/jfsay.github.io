---
title: "防止文件被改写的简单实现方式"
date: 2014-10-13
categories: 
  - "software_programming"
tags: 
  - "vb"
---

最近在写的一个小程序中有个配置文件，这个文件对整个程序来说是至关重要的，如果它被删除或者改写的话，整个程序无法运行，或者运行后无法关闭。所以我一直在寻找如果让手工无法改写文件的方法。

对于“删除”来说是很容易解决的，程序中查找配置文件的路径，若为空则创建，并给些默认值。VB的示例代码如下：

```
FileName = App.Path + "\CONFIG"
'如果文件不存在，则创建文件
If Dir(FileName) = "" Then
     Open FileName For Output As #1 '打开顺序文件，我们可以使用Open语句
     a = Encode("123") + vbCrLf + "10" + vbCrLf 'vbCrLf为回车
     Print #1, a '写数据
     Close #1 '关闭文件       
End If

```

对于手工改写配置文件，我一直无能为力，我试图在程序中把该文件隐藏掉。VB的示例代码如下：

```
SetAttr FileName, vbSystem Or vbHidden '隐藏文件

```

但终归来说是治标不治本，文件仍然会被改写的。然后我想到修改配置文件后缀法，让人手工没那么容易打开文件，但是总是有方法打开的。最终让我想到一个简单的解决方法是，在程序中先打开配置文件，之后手工就无法打开了。VB的示例代码如下：

```
Open FileName For Binary As #99

```

只是记得程序在改写该文件时要先关闭打开的文件，不然改写会失败的。VB的示例代码如下：

```
Close #99 '关闭文件

```

总结一下，防止文件被改写的简单实现方式就是在程序中先打开该文件。完整的程序示例可参考[这里](https://www.jfsay.com/archives/970.html "屏幕锁PcLocker更新")。
