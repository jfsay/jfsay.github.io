---
title: "PHP和JS的几点总结"
date: 2010-06-14
categories: 
  - "website"
tags: 
  - "php"
---

1、Javascript的值传给php来处理可以把这个值放在一个hidden表单里面，例如：

```
<form>
<input type="hidden" name="myclass" id="myclass" value="" />
<form/>
<---javascript>
form.myclass.value = classString;
<---javascript>
```

这样的话就把classString的值传给了name是myclass的隐藏的表单。

2、数据库查找的时候是精确查找，一定要注意查找的字符串中的空格，今天我被这个问题快整崩溃了，怎么着都不对，又找不到错误，例如：

```
$array = @explode(“”,$class); //把$class分解并放到$array数组中
```

我没有想到这个分解的字符串中存在的空格。具体的过程是这样的：

比如给一段字符串：abc

分出来的字符串为：a,b,c, ,

c后面是存在空格的。

我在数据库中查找的时候总是不对，错误就在这里了。

3、表单提交按钮中的return

有return的语句

```
<input type="submit" name="Submit" value="完成" onclick="return checkEmpty(this.form)" />
```

无return的语句

```
<input type="submit" name="Submit" value="完成" onclick="checkEmpty(this.form)" />
```

上面两条语句的区别就是：有return时，当funtion返回false时，网页不提交。

  
4、JS中使用<!— —>的作用是注释，主要为了支持老版本的浏览器。

  
5、表单中的关键字

```
<input type="hidden" name="class" id="class" value="" />
```

上面的语句中出现了“class”的关键字，调试的时候除了问题，我怎么找都没有找到错误。所以给表单中的元素命名时最好不要使用关键字，比如：

```
<input type="hidden" name="myClass" id="myClass" value="" />
```
