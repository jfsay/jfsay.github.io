---
title: "安卓实现APP2SD的步骤"
date: 2012-02-25
categories: 
  - "software_programming"
tags: 
  - "android"
  - "app2sd"
  - "moto"
  - "xt502"
  - "手机"
---

安卓2.2以下的系统，应用程序只能安装在手机内部存储中，而不能安装在SD卡中。手机的存储空间毕竟有限，于是出现了APP2SD（Application to SDcard）方法，这样就可以把应用程序装在SD卡中了。

**本人测试的机器配置：**

1、Android2.1

2、MOTO XT502

3、机身剩余存储容量172MB（手机的ROM为512MB，被系统占用了绝大部分）

4、SD卡的存储空间为2GB

**具体的步骤是：**

**（1-7为SD卡分区，8-11为复制文件，12-17为命令操作）**

1、SD卡放入读卡器中，并连接电脑。

2、电脑下载分区工具gdisk\_sd.rar，解压缩，运行sd\_gb.cmd程序。

3、选择箭头所指的DISK编号。

4、选择“切出app2sd所需的EXT2磁区”。

5、“输入fat32分区容量”，也就是SD卡中安装应用程序外的空间大小，我采用的是2GB-600MB=1400MB，所以输入的是1400.

6、等待完成。

7、SD卡插入手机中。

8、电脑下载APP2SD.zip文件，并解压（例如解压后的文件夹名称为APP2SD），然后拷贝到SD中。

9、手机下载“Z4root”应用程序，使得手机获得Root权限。成功之后会出现superuser（超级权限）的图标。

10、手机下载“RE管理器”应用程序。使用它把SD卡中APP2SD文件夹中的所有文件拷贝到system/xbin中。

11、手机设置“USB 调试”模式，具体位置是：设置→应用程序→开发→

12、电脑下载tool.rar，解压缩，运行Dos\_Console.bat批处理程序。

13、输入：adb shell

14、在$的后方输入：su

15、手机中出现“ROOT权限的请求”，选择“Allow"同意。

16、这时su下出现＃，依次输入（可以复制粘贴）以下三条语句，然后回车。

chmod 4755 /system/xbin/\*

chown root.shell /system/xbin/\*

sh /system/xbin/app2sd.sh

17、完成，SD卡插入手机。此后，手机不用做任何设置，应用程序会自动安装到ext2分区中。

注：以上步骤看似繁琐，实际操作起来极其简单，只需按部就班。具体的图文教程可参照[xt502最详细完整的APP2SD教程，2.2系统也适用](http://bbs.hiapk.com/thread-585226-1-1.html)。
