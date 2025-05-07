---
title: "网站空间使用cPanel进行数据库自动备份的方法"
date: 2010-07-31
categories: 
  - "website"
tags: 
  - "空间"
---

对于网站站长来说，网站空间数据的备份可谓是头等大事。首先，你不能保证网站服务器能经得起百年一遇的故障。其次，你不能阻止别有用心的人对你的网站胡作非为。 网站建好之后，数据库可谓是网站的核心，对他的优化和备份尤显重要，下面来介绍一下使用cPanel的时钟任务进行数据库的备份。

### 数据库优化

进入cPanel，再进入“时钟守护作业”，在“Common Settings”选择好命令运行的时间周期，在“Command”中填入以下语句：

mysqlcheck -Aao --auto-repair -u\[数据库名\] -p\[数据库密码\]

**上面的数据库名和密码一定要紧挨着u和p，中间没有空格(下同)。**

### 数据库备份

1、在FTP根目录下新建一个文件夹目录，比如命名为backup。

2、在本机新建一个dbbackup.sh的文件，内容如下：

```
cd /home/[username]/backup #切换到工作目录 
stamp=$(date +%y%m%d) #獲得當前時間
mysqldump -u[数据库用户名] -p[数据库密码] [数据库] > db_backup_$stamp.sql #導出數據庫
bzip2 -z -9 -f db_backup_$stamp.sql #壓縮數據庫
mutt [邮箱地址] -a db_backup_$stamp.sql.bz2 -s "database backup" #郵件發送
rm db_backup_$suffix.sql.bz2 #移除臨時文件
```

3、使用FTP上传工具，把上传dbbackup.sh文件上传到backup文件夹中。注意传输模式为ASCII，不然会出错。

4、修改dbbackup.sh的权限为755。修改方法：cPanel中找到“文件管理器”，选择dbbackup.sh文件并修改权限。

5、cPanel中进入“时钟守护作业”，设置好运行时间，然后在“Command”中填入dbbackup.sh的路径，如下所示：/home/username/backup/dbbackup.sh
