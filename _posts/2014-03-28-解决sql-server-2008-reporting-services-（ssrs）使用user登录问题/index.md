---
title: "解决SQL Server 2008+ Reporting Services （SSRS）使用USER登录问题"
date: 2014-03-28
categories: 
  - "software_programming"
tags: 
  - "reporting-services"
  - "sql-server"
---

我的数据库和报表服务的版本如下：

数据库：SQL Server 2008 R2 报表服务：SQL Server 2008 R2 Reporting Services

我本想让用户像访问网站一样访问我的报表服务，该死的SQL Server Reporting Services从2005以后就不依赖于IIS，造成用户不能匿名访问了。

网上有关于“SQL Server 2008 Reporting Services匿名访问”的教程，通过修改Reporting Services下的配置文件来实现，我对着着教程做了一遍，没有成功。

突然想到，我只是让有权限的USER账号能访问就行，没必要实现匿名访问。当别人用别的计算机访问该服务时总是提示“没有权限”，而把这个人的账号加入服务器的Administrators组里面时就能访问了，别的组却都不能访问。于是想到会不会是Reporting Services的配置项的访问权限只对Admin开放？之后证明我的推断是正确的，也让我找到了SSRS使用USER登录的方法，步骤如下：

1、用Administrator进入报表管理器URL：http://localhost/Reports 2、主文件夹的“安全性”，新建角色分配，把Users组加进去 3、进入右上角的“站点设置”，新建角色分配，把Users组加进去 4、进入“文件夹设置”，新建角色分配，把Users组加进去

也就是把Users组加入站点和文件夹的相应权限当中去。

总算解决了，差点就把数据库装回SQL Server 2000了。

参考：http://www.soheib.com/technical-knowledge/sql-server-2012-reporting-services-uac-user-access-control/
