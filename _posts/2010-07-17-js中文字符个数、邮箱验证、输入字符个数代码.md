---
title: "JS中文字符个数、邮箱验证、输入字符个数代码"
date: 2010-07-17
categories: 
  - "website"
tags: 
  - "js"
---

JS计算字符串中的中文字符个数，这里采用的是先去掉非中文字符，再返回length属性。代码如下：

```
 
<script type="text/javascript"> 
/******************************************************
* Share JavaScript (http://www.ShareJS.com)
* 使用此脚本程序，请保留此声明
* 获取此脚本以及更多的JavaScript程序，请访问 http://www.ShareJS.com
******************************************************/
 
 function cLength(str){ 
 var reg = /[^\u4E00-\u9FA5\uf900-\ufa2d]/g; 
 //匹配非中文的正则表达式 
 var temp = str.replace(reg,''); 
 return temp.length; 
 } 
 var str = "中文123"; 
 document.write(str.length+'<br />'); 
 document.write(cLength(str)); 
 </script>
```

JS实现邮箱验证的代码：

```
 
var strm = myForm.inpEmail.value //提交mail地址的文本框
 var regm = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/;//验证Mail的正则表达式,^[a-zA-Z0-9_-]:开头必须为字母,下划线,数字,
	if (!strm.match(regm) && strm!="")
	 {
	 alert("邮箱地址格式错误或含有非法字符!再来修改一下。");
	 myForm.inpEmail.focus(); 
	 return false;
	 }
```

JS判断输入的字符数个数的代码：

```
 
if(myForm.txaArticle.value.length>1000){
 alert("写的内容太多了，稍微修剪点吧！"); 
 myForm.txaArticle.focus(); 
 return false;
}
```
