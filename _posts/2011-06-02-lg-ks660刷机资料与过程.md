---
title: "LG KS660刷机资料与过程"
date: 2011-06-02
categories: 
  - "software_programming"
tags: 
  - "手机"
---

入手LG KS660快一年了，这是一款貌似智能机的弱智机。都说LG的产品中看不中用，这次算是领教过了。

**刷机的原因**

1、  LG KS660的触摸屏越用越不灵敏，时灵时不灵，几乎到了无法忍受的程度。

2、  原机是“中国移动”定制的版本，安装了太多中国移动的垃圾软件，而且其中99.99%都是没用的玩意。

**刷机的软件**

1、  [MultiGSM Ver3.0.rar](https://docs.google.com/leaf?  id=0BylPy_4csyrXNmIxOWU1MDctYTQ5Ny00NDdjLTljMmQtMzcxZjdkZjM2ZDlm&hl=zh  _CN )（刷机平台）

2、  [KS660AT-00-V10i-CIS-XXX-SEP-03-2009\_0\_ROM .zip](http://www.gsm-data.com/lg/summary/816/2031.html)（刷机包/固件）

**刷机的过程**

1、  手机取下SIM卡、储存卡、电池。

2、  安装驱动：C:\\GSMULTI\\UsbDrivers\\INFINEON下的Setup.exe文件运行。

3、  USB端口映射

- C:\\GSMULTI下的USBMap\_V01.exe运行。
- 选择INFINEON.
- 点击MAPPING START.
- 手机与电脑连接。
- 等待出现一串数字后点击SAVE&EXIT.

4、  运行MULTIGSM\_v3.0

- 选择setting下的configuration，在 DLL和S/W中中添加刷机包中的相应文件。
- 点击START.
- 手机与电脑连接。
- 开始刷机，等待完成。

**刷机的效果**

- 触摸屏灵敏了
- 该死的“中国移动”的垃圾全都没有了
- 界面语言是全英文的，不过支持中文输入
- 电话薄不支持中文条目的首字母查找

参考：用xp、vista和win7系统刷机（gsm multi平台、轻松解决定屏）
