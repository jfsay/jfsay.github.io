---
title: "C#将文件复制到指定文件夹，并按日期归档"
date: 2014-05-14
categories: 
  - "software_programming"
tags: 
  - "c"
  - "复制"
  - "文件"
---

下面是在C#中将文件复制（剪切是先复制再删除）到指定的路径，并按日期归档的一个简单实例。值得注意的2点是：

1）文件的路径是关键，程序中使用双斜杠\\\\

2）文件和文件夹的区别

```
private void DoWork()
{
      String dir="D:\\ABC"
      //创建备份文件夹，按时间命名    
      String bakDir = dir + "\\bak\\" + DateTime.Now.ToString("yyyy-MM-dd");

     if (Directory.Exists(bakDir) == false){
              Directory.CreateDirectory(bakDir);
     }
     string[] files = Directory.GetFiles(dir);
     if (files.Length != 0) {
           foreach (string file in files) {
           FileInfo fileinfo = new FileInfo(file);
           try{
               string fileName = file.Replace(dir, "");
               //备份文件
               File.Copy(file,Path.Combine(bakDir,fileName));
               File.Delete(file);
           }    
     }
}
```
