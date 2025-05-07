---
title: "Access使用VBA实现表或查询每相邻两行字段相减"
date: 2017-02-06
categories: 
  - "software_programming"
tags: 
  - "vb"
---

为了实现如下的功能：表或查询每相邻两行字段相减。例如下面的这张表或查询，结果是成绩列的每两行相减。

姓名 学号 成绩  
小王 001 240  
大王 002 260  
小王 001 280  
大王 002 290  
大王 002 260

思路如下：  
1、先把表另存一份表1，加一个自增长的ID。  
2、表1再另存一份表2。  
3、表1和表2用“表1的ID=表2ID-1”来连接，就是相邻两行连接起来。  
4、将上面的连接表成绩字段相减，再另存一份。  
5、删除表1和表2. 

<!--more-->

[示例模板下载](https://drive.google.com/open?id=0BylPy_4csyrXSlc3bFpFWnZDd0k)

代码如下：

```
Option Compare Database

Private Sub Command0_Click()
    On Error GoTo Err_Command0_Click
    
    Dim TableName, FieldName, Temp_TableName, Temp_TableName_2, NewTableName As String '变量定义,分别表示表名 字段名 临时表 临时表2 生成新表表名
    
    TableName = Trim(Text7) '表名
    FieldName = Trim(Text9) '字段名
    Temp_TableName = "Temp_" & TableName '临时表
    Temp_TableName_2 = "Temp_" & TableName & "_2" '临时表2
    NewTableName = "New_" & TableName & FieldName '生成新表表名
    
    
    str1 = "select * into " & Temp_TableName & " from " & TableName '将查询或表另存为临时表
    
    str2 = "Alter table " & Temp_TableName & " Add column ID counter (1,1)" '增加字段ID,自增长
    
    str3 = "select * into " & Temp_TableName_2 & "  from " & Temp_TableName '将临时表复制一份
    
    CurrentDb.Execute (str1) '执行上述三条SQL语句
    
    CurrentDb.Execute (str2)
    
    CurrentDb.Execute (str3)
    
    '将临时表和临时表2用ID连接,然后另存为新表
    
    str4 = "select * into " & NewTableName & "  from ( select [" & Temp_TableName & "].*,[" & Temp_TableName_2 & "]." & FieldName & "-[" & Temp_TableName & "]." & FieldName & " AS " & FieldName & "_差值 from " & Temp_TableName & "  left Join " & Temp_TableName_2 & " on [" & Temp_TableName & "].ID = [" & Temp_TableName_2 & "].ID-1)"
    
    CurrentDb.Execute (str4) '执行上述SQL语句
    
    MsgBox "新表已生成，请稍后按F5刷新", vbOKOnly, "完成提示"
    
    DoCmd.Close '关闭当前窗口
    
    
    CurrentDb.Execute ("drop table " & Temp_TableName & "") '删除临时表
    CurrentDb.Execute ("drop table " & Temp_TableName_2 & "")  '删除临时表2

Exit_Command0_Click:
    Exit Sub

Err_Command0_Click: '上述语句执行出错的话,跳转到这里:类似于TRY CATH的功能(VBA没有)
    MsgBox Err.Description
    CurrentDb.Execute ("drop table " & Temp_TableName & "") '报错的话删除复制的临时表
    CurrentDb.Execute ("drop table " & Temp_TableName_2 & "")
    Resume Exit_Command0_Click
    
End Sub
'取消按钮事件,关闭窗口
Private Sub Command11_Click()
   DoCmd.Close
End Sub
```
