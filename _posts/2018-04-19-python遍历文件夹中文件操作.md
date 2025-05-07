---
title: "Python遍历文件夹中文件操作"
date: 2018-04-19
categories: 
  - "software_programming"
tags: 
  - "python"
---

以下代码实现遍历D盘test文件夹下的所有文件，得到所有文件的路径。为防止Windows下转义字符的干扰，文件路径改为反斜杠/的形式，使用path=path.replace("\\\\", "/")将得到的文件路径转换为反斜杠形式。

```
import os

rootdir = 'D:/test'
#列出文件夹下所有的目录与文件
list = os.listdir(rootdir)
for i in range(0,len(list)):
path = os.path.join(rootdir,list[i])
if os.path.isfile(path):
path=path.replace("\\", "/")
print(path)
```
