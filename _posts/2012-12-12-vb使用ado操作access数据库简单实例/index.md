---
title: "VB使用ADO操作Access数据库简单实例"
date: 2012-12-12
categories: 
  - "software_programming"
tags: 
  - "access"
  - "ado"
  - "vb"
---

这里只是个简单不能再简单的VB小程序实例，但它包含这几个关键字：VB6.0、ADO、Access

环境：visual basic 6.0 企业版（非精简版，不然会缺少必须的控件）

数据库：Access数据库，数据库是xs.mbd，内建表为xj

结果：vb使用ADO连接access数据库，查询xj表中的所有数据，然后把查询到的结果循环输出到窗口中。

代码：

```
Private Sub Form_Click()
Dim db As New ADODB.Connection, RS As New ADODB.Recordset 'ADO连接对象和记录集
Dim strSQL As String 'SQL字符串
db.ConnectionString = "provider=Microsoft.Jet.OLEDB.4.0;Data source =" & App.Path & "/xs.mdb" '数据库连接
db.Open '打开数据库

strSQL = "select * from xj" 'SQL字符串
RS.Open strSQL, db, 3, 1 '查询数据表
Do While Not RS.EOF '循环输出查询到的结果
Print RS!姓名; RS!性别; RS!班级; RS!出生年月 '在窗口中打印输出结果
RS.MoveNext '记录下移
Loop
RS.Close '关闭记录集
Set RS = Nothing
End Sub
```

源代码下载地址：[vb\_ado\_access.zip](https://docs.google.com/open?id=0BylPy_4csyrXQmhhT1BqUHlDYjQ)
