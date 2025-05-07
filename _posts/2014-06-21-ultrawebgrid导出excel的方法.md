---
title: "UltraWebGrid导出Excel的方法"
date: 2014-06-21
categories: 
  - "software_programming"
tags: 
  - "c"
  - "excel"
  - "ultrawebgrid"
---

这段时间需要用C#做个页面，把网格中查询出来的数据导出到Excel中。在网上找了一大堆C#导出Excel的代码，试来试去都不可用。好多代码是针对.net 2.0或者3.0的，无奈我的程序用的是.net 1.0开发的，造成好多函数都不能用。之后就转变思想，寻找“UltraWebGrid导出Excel的方法”，在CSDN中找到一批流传甚广的文本，可是我人肉测试的结果还是不能用。就在我近乎绝望的时候，我发现原来UltraWebGrid自带导出Excel的控件。使用也很简单，前端注册，后台调用就行了。以下是一个简单的实例。

PS：UltraWebGrid的中文文档真的太少了，使用起来很不方便。

modle.aspx的代码如下，第1行注册控件，第2行添加一个导出按钮，第3行添加UltraWebGridExcelExporter控件。

```
<%@ Register Assembly="Infragistics.WebUI.UltraWebGrid.ExcelExport.v5.1, Version=5.1.20051.37, Culture=neutral, PublicKeyToken=7dd5c3163f2cd0cb" Namespace="Infragistics.WebUI.UltraWebGrid.ExcelExport" TagPrefix="igxl" %>
<asp:button id="Button2" runat="server" Text="导出" Width="64px"></asp:button>
<igxl:UltraWebGridExcelExporter ID="UltraWebGridExcelExporter1" runat="server" DownloadName="Workbook1.xls"></igxl:UltraWebGridExcelExporter>
```

modle.aspx.cs代码如下，定义UltraWebGridExcelExporter，然后调用Export函数。

```

protected Infragistics.WebUI.UltraWebGrid.ExcelExport.UltraWebGridExcelExporter UltraWebGridExcelExporter1;
private void Button2_Click(object sender, System.EventArgs e){
        UltraWebGridExcelExporter1.Export(this.UltraWebGrid1);                    
}
```
