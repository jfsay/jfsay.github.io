---
title: "MOTO XT536手机ROOT及安装谷歌服务包"
date: 2012-11-05
categories: 
  - "software_programming"
tags: 
  - "android"
  - "root"
  - "xt536"
---

MOTO XT536的官方ROM中存在大量的垃圾应用，并且删除掉了包括Google框架在内的谷歌服务包。为了使用上优质的谷歌服务，我又折腾了。

#### ROOT

以前我的安卓2.1和2.2的版本是通过Z4root等一键Root工具来把手机ROOT的，我天真的以为MOTO XT536也可以使然。没想到尝试过了网上流传的一键Root工具后，都没有成功。下面陈述一下成功的做法吧。

1、手机卸载SD卡：设置-存储-SD卡卸载或者拔出SD卡

2、手机开启USB调试：手机设置->应用程序->开发勾选USB调试

3、电脑下载并安装XT536/535驱动（[下载地址](https://docs.google.com/open?id=0BylPy_4csyrXb1FuYlNCdVBIRGc)）

4、电脑下载并安装安装SUT LR (Soft Update Tool LR)

5、电脑下载XT536/535的ROOT工具包，其中包含FXX\_PR3\_NV.xml和NvDefinition.xml这两个主要文件，缺一不可，不然会报错。（[下载地址](https://docs.google.com/open?id=0BylPy_4csyrXZmY3dTI4MWZYSlk)）

6、电脑下载并安装SuperOneClick程序

7、手机连电脑，电脑运行SUT LR程序，点击“NEXT”，选择ROOT工具包中的FXX\_PR3\_NV.xml文件，安装完成。

8、电脑运行SuperOneClick程序，点击“Root”按钮，运行完毕。

9、重启手机

#### Root Exploer

Root exploer可谓是安卓上的最具杀伤力的工具了，用它可以来操作几乎安卓上的任何文件。所以它应该是手机获得Root以后必装的工具之一。

但是我的手机在Root之后，运行Root exploer却意外停止，只能强行关闭。卸载重装Root exploer问题也没有解决，最后发现原来是它的版本问题，通过安装最新的版本之后问题得到解决。

#### 谷歌服务包

万恶的手机制造商删除掉了谷歌服务包，这就使得谷歌的大部分软件不能使用。下面陈述一下安装谷歌服务包的方法。

1、电脑下载Android 2.3.7对应的谷歌服务包（[下载地址](https://docs.google.com/open?id=0BylPy_4csyrXZ01pZTNTOVlldTA)）

2、电脑解压缩后，复制文件夹到手机的SD卡中

3、手机使用Root exploer把该文件夹中的所有文件复制到system/app目录下，同时把文件的权限改为211

4、重启手机
