---
title: "ACCESS使用VBA实现列值累加并取得累加阀值的记录"
date: 2014-08-06
categories: 
  - "software_programming"
tags: 
  - "access"
  - "vb"
---

题目很拗口，主要是想要表达的东西比较曲折，还是以实例来说明比较直观，假设在Access中有以下的表table1。table1是一张成绩表，我想要的结果是：所有人的成绩按着总分（Score）从大到小排列，然后在排列好的表中从上到下累加English/Score列（第1行+第2行+……+第N行的值），当累加值>0.7时，取出第1行到第N行的记录。

<!--more-->

| Name | English | Frence | Chinese | Score | Proportion    (English/Score)   |
| --- | --- | --- | --- | --- | --- |
| Jasmine | 81 | 40 | 100 | 220 | 0.37 |
| Hill | 70 | 80 | 60 | 210 | 0.33 |
| Jay | 80 | 20 | 80 | 180 | 0.44 |
| Tom | 50 | 50 | 50 | 150 | 0.33 |

VBA的代码思路是：先把Table1按总分（Score）从大到小排列取出来放在记录集中，然后通过循环累加Proportion的值，取出符合条件的行数，最后从记录集中取出所需的内容。

代码如下：

```
Sub LookupSum()
   Dim rst As Recordset   
   Dim MARK As Double
   Dim values AS Double '阀值
   Dim num As Double    '行数
   Dim qdf As QueryDef  '查询
   Dim strSQL As String
 
   MARK = 0
   num= 0
   values = 0.7
   '从大到小排列取出来放在记录集中
   Set rst = CurrentDb.OpenRecordset(" select * from table1 order by Score desc")
   '循环累加Proportion的值
   Do While Not rst.EOF
      If MARK >= values Then Exit Do
          MARK = MARK + rst! Proportion
          num = num + 1
          rst.MoveNext
   Loop
  '新建一个查询
   strSQL = "select top "  & num & " * from table1 order by Score desc"
   Set qdf = CurrentDb.CreateQueryDef("查询累计比例大于70%的成绩", strSQL)
   DoCmd.OpenQuery qdf.Name
End Sub
```
