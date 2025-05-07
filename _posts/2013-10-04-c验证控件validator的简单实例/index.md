---
title: "C#验证控件validator的简单实例"
date: 2013-10-04
categories: 
  - "software_programming"
tags: 
  - "c"
---

ASP.NET为开发人员提供了一套简单实用的服务器控件来验证用户输入的信息是否有效。这些控件的主要属性有id（控件的唯一id）、ControlToValidate（被验证的控件的id）、ErrorMessage（当验证失败时，在控件中显示的文本）、runat（规定该控件是一个服务器控件。必须设置为 "server"）。

1、RequiredFieldValidator：验证一个必填字段，如果这个字段没填，那么将不能提交信息。

下例为文本框输入是否为空的验证，输入内容为空时报错。代码如下：

```
<ASP:TextBox id="txtName" RunAt="Server"/>
<ASP:RequiredFieldValidator id=" RequiredFieldValidator1" Runat="Server" 　ControlToValidate="txtName" 　ErrorMessage="用户名不能为空"  ForeColor="red">*</ASP:RequiredFieldValidator>
```

2、CompareValidator：比较验证。比较两个字段值是否相等，如密码和确认密码两个字段是否相等；比较一个字段与一个具体的值。

下例为两个文本框的输入密码验证，如果两个文本框输入内容不一致时报错。代码如下：

```
<asp:TextBox ID="txtPWD1" runat="server" TextMode="Password"></asp:TextBox>
<asp:TextBox ID="txtPWD2" runat="server" TextMode="Password"></asp:TextBox>
<asp:CompareValidator ID="CompareValidator1" ForeColor="Red" runat="server" ErrorMessage="两次密码输入不一致" ControlToValidate="txtPWD1" ControlToCompare="txtPWD2"    type="String">
```

下例为文本框输入内容值验证，如果输入内容和某值相等时报错。代码如下：

```
<ASP:TextBox id="txtName" RunAt="Server"/>
<ASP:CompareValidator id=" CompareValidator1" Runat="Server" 　ControlToValidate="txtName" ControlToCompare="123"　ErrorMessage="该用户已注册"  Operator="NotEqual"　 type="String"  ForeColor="red"></ASP:CompareValidator>
```

3、RangeValidator：范围验证。验证一个字段是否在某个范围中。

下例为文本框输入的内容在最大值和最小值之间，如果超过最大或最小值时报错。代码如下：

```
<asp:TextBox ID="num_id" runat="server" BackColor="White"></asp:TextBox>
<asp:RangeValidator ID="RangeValidator1" runat="server" ErrorMessage="编号为1~1000之间" ControlToValidate="num_id" MaximumValue="1000" MinimumValue="1" Type="Integer"></asp:RangeValidator>
```

4、RegularExpressionValidator：正则表达式验证。它根据正则表达式来验证用户输入字段的格式是否合法，如电子邮件、身份证、电话号码等。

下例为文本框输入内容符合ValidationExpression中正则表达式的要求，如果不符合要求时报错。代码如下：

```
<asp:TextBox ID="txtMail" runat="server" BackColor="White"></asp:TextBox>
<asp:RegularExpressionValidator ID="RegularExpressionValidator1" ForeColor="Red" runat="server" ErrorMessage="请输入正确的邮箱" ValidationExpression="\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*" ControlToValidate="txtMail"></asp:RegularExpressionValidator>
```
