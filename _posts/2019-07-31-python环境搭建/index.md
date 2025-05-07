---
title: "Python环境搭建"
date: 2019-07-31
categories: 
  - "software_programming"
tags: 
  - "python"
---

一、安装Python软件，加入环境变量

测试Python是否安装成功：cmd - python

二、 安装包

在使用python时经常可以发现某个lib有whl、tar、tar.gz等格式的包。

whl包：已经编译的包，类似于exe文件；

tar包：源文件，只是打包在一起，还没有编译；

tar.gz包：源文件，压缩并打包在一起，还没有编译。

一般网络好的情况下，直接pip在线安装。 如果环境挺充足，可以用tar包或者tar.gz包；如果环境欠缺，比如缺少某些编译环境，或者想要快速且稳定，就得用whl包。

1 在线安装

pip install xxx

2 下载安装

2.1 如果下载得到的是.tar.gz压缩包，解压，在解压目录的当前文件夹下，打开DOS命令运行：python setup.py install

2.2 .whl文件安装：当前目录下运行：pip install xxx.whl

三、执行Python脚本

1、直接在DOS命令运行Python xxx.py

2、封装成bat文件

@echo off

start python qd\_am.py

exit

3、编制成exe

3.1 安装pyinstaller

3.2 编译pyinstaller -F -w game.py  （-F表示打包单个文件，-w是为了打开exe时候不弹出黑框）

3.3 设置exe的图标 pyinstaller -F -w -i bitbug\_favicon.ico game.py（-i用来设置编译成exe文件的图标，后面跟.ico格式的图片文件）
