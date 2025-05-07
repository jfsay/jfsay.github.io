---
title: "Oracle与SQL Server区别"
date: 2018-05-14
categories: 
  - "software_programming"
tags: 
  - "oracle"
---

**实例**

SQL Server实例是安装SQL Serve数据库软件时生成，代表一个包含了操作系统文件、内存结构、后台进程以及注册表信息的独立的应用服务。在Windows系统中用一个存在着停止和运行状态的服务来代表一个实例，当处于运行状态时，实例要占用一定的服务器内存以及生成一定数量的后台进程。一般情况下我们安装SQL Server2008就只有默认的一个实例，实例名为MSSQLSERVER，如果我想要安装多个实例那么就要再次安装sqlserver数据库，也就是需要多少个实例就安装多少次，然后安装过程中修改实例名如MSSQLSERVER1。

Oracle就不用这么麻烦，可以按需要创建多个实例。

**数据库**

从物理角度说，一个SQL Server数据库表现为存储于磁盘上面的一组操作系统文件的集合。数据库文件分为两种：数据文件(data file)和事务日志文件(transaction log file)。一个数据库至少要包含一个数据文件和一个事务日志文件，SQL Server数据库的资料主要是存在于数据文件中，事务日志文件用来记录发生在这些数据上面的变更记录，SQL Server在执行系统恢复的时候要用到它。一个数据文件或事务日志文件只能隶属于一个特定的数据库，不存在两个数据库共用一个数据文件或者是日志文件的情况。一个数据量很大的数据库可以使用多个数据文件，这些数据文件能够被逻辑的组合成一个称为文件组(file group)的逻辑组。

**表空间**

在SQL Server中逻辑分组由数据库自己来完成，而在Oracle中，这项工作由表空间(tablespace)完成，Oracle表空间是用来对表、视图、索引和其他数据库对象进行分组的逻辑结构。例如，你的Oracle产品库可以给HR应用一个单独的表空间，支付应用则使用另外一个。一个数据库可以逻辑的分成若干个表空间，这些表空间在物理上则由一个或者多个数据文件组成。**因此在Oracle中与SQL Server数据库等价的是表空间**。

**用户**

Oracle数据库里面用户是独立的，不同的用户下面对应SQL Server里面的数据库，每个用户就相当于SQL Server里面的一个独立数据库，在Oracle里面你可以为自己的用户分配独立的空间，大小可以自由设置。SQL Server里面的用户不和数据库绑定的。

Oracle 是单实例单数据库多个表空间，SQL Server是一个实例下建立多个数据库，Oracle中与SQL Server数据库等价的是表空间。

Oracle创建一个数据库/表空间需要以下三个步骤**（**Oracle在创建数据库/表空间的时候要对应一个用户，数据库/表空间和用户一般一一对应**）**：

1.创建数据库/表空间的文件

```
CREATE TABLESPACE monitor LOGGING DATAFILE 'E:\app\owner\oradata\orcl\monitor.dbf' 
SIZE 100M AUTOEXTEND ON NEXT 32M MAXSIZE 500M EXTENT MANAGEMENT LOCAL;
 
CREATE TEMPORARY tablespace monitor_temp tempfile 'E:\app\owner\oradata\orcl\monitor_temp.dbf'
size 100m autoextend on next 32m maxsize 500m extent management local;
```

2.创建用户与上面创建的文件形成映射关系

```
CREATE USER monitor IDENTIFIED BY monitor 
DEFAULT TABLESPACE monitor 
TEMPORARY TABLESPACE monitor_temp;
```

3.给用户添加权限

```
grant connect,resource,dba to monitor;
grant create session to monitor;
```
