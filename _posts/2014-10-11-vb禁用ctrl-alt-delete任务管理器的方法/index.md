---
title: "VB禁用Ctrl-Alt-Delete/任务管理器的方法"
date: 2014-10-11
categories: 
  - "software_programming"
tags: 
  - "vb"
---

在Windows XP下禁用Ctrl-Alt-Delete的方法比较简单，因为Ctrl-Alt-Delete组合键的功能就是调用任务管理器，直接把任务管理器给禁用了，Ctrl-Alt-Delete的功能也就没有了，相当于也给禁用了。这个方法的简单的实现是用二进制 stream 形式先打开 C:\\windows\\system32\\taskmgr.exe任务管理器程序，使后续无法手工正常打开任务管理器。代码如下：

```
Open "C:\WINDOWS\system32\taskmgr.exe" For Binary As #1
```

这种方法在XP上是可行的，但是在VISTA和WIN7上是无效的。我的解决方法是用taskkill命令来结束任务管理器程序taskmgr.exe。代码如下：

```
Shell ("cmd /c taskkill /f /im taskmgr.exe"), vbHide
```

在VB程序里实现的话，最好把上述语句放到Timer事件中，每隔一段时间执行一次，就能实现禁用任务管理器的目的了。代码如下：

```
Private Sub Timer1_timer()
    Shell ("cmd /c taskkill /f /im taskmgr.exe"), vbHide
End Sub
```
