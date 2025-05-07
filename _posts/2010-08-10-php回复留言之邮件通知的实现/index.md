---
title: "PHP回复留言之邮件通知的实现"
date: 2010-08-10
categories: 
  - "website"
tags: 
  - "php"
---

浏览网页留下了自己的评论脚印，或者是在问答系统中提出了问题，之后有人回复了你的留言或者回答了你提出的问题，这时候我们总是希望通过邮件来通知一下。其实PHP实现起来极其得简单，只需要Mail函数就可以来实现。

mail()函数：作用是寄出电子邮件。  
语法: boolean mail(string to, string subject, string message, string \[additional\_headers\]);  
to 指定的邮件地址，subject 表示主题，message 为信件内容。额外的选项 additional\_headers 可省略，表示其它的邮件文件头。

例如：mail(123@example.com,"你的评论有人回复了","回复的内容是：balabala……",456@example.com)

当然我们不想回复的内容就是简单的一句话，希望它尽量丰富些，比如说有只想网站的超链接。

可以把message定义为

```
$message = '
<html>
<head>
 <title>Birthday Reminders for August</title>
</head>
<body>
 <p>Here are the birthdays upcoming in August!</p>
 <table>
 <tr>
 <th>Person</th><th>Day</th><th>Month</th><th>Year</th>
 </tr>
 <tr>
 <td>Joe</td><td>3rd</td><td>August</td><td>1970</td>
 </tr>
 <tr>
 <td>Sally</td><td>17th</td><td>August</td><td>1973</td>
 </tr>
 </table>
</body>
</html>
';
```

另外，邮件主题或者内容中是中文的话，接收到的邮件总会出现乱码的现象。
