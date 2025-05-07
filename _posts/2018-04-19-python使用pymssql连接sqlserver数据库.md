---
title: "Python使用pymssql连接SQLServer数据库"
date: 2018-04-19
categories: 
  - "software_programming"
tags: 
  - "python"
---

一、下载对应Python版本的pymssql包

pymssql包的名字一般如下pymssql-2.1.4.dev5-cp36-cp36m-win\_amd64.whl，其中cp36代表Python3.6版。

二、安装pymssql包

开始-运行-CMD-pip install E:\\Downloads\\pymssql-2.1.4.dev5-cp36-cp36m-win\_amd64.whl

三、连接SQLServer数据库（以下查询需要先建立数据库）

```
import pymssql

conn=pymssql.connect(host='10.0.0.1',user='sa',password='test',database='test')
'''
如果和本机数据库交互，只需修改链接字符串
conn=pymssql.connect(host='.',database='Michael')
'''
cur=conn.cursor()
cur.execute('select * from test')
#如果update/delete/insert记得要conn.commit()
#否则数据库事务无法提交
#conn.commit()
print (cur.fetchall())
cur.close()
conn.close()
```
