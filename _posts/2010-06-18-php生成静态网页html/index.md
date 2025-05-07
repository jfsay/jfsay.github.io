---
title: "PHP生成静态网页HTML"
date: 2010-06-18
categories: 
  - "website"
tags: 
  - "php"
---

PHP生成静态网页HTML方法分为生成伪静态HTML和生成真正静态的HTML.

伪静态可以使用.htaccess重定向来实现：

```
RewriteEngine on
RewriteRule ([0-9]{1,}).html$ detail.php?nid=$1
```

上面表示遇到“数字+html”，页面跳转到“detail.php”，然后把括号里的参数给“$1”。比如99.html就会跳转到datail.php?nid=99，这样就实现了伪静态html页面了，不是真正的静态页面。

真正的静态html，是使用php来生成html页面。对于那种网站访问量大的大站，一般采用这种方式。 下面介绍一种简单的方法的例子，两个文件：add.php和model.php

model.php

```
此新闻的标题:{title} 
此新闻的内容:{content} 
```

add.php：

```
<?php 
 require_once("conn.php"); //引用conn.php，连接数据库
 $title="我是标题";
 $content="我是内容"; //获得表单变量 
 //以下建立一文本文档，其值自动计数
 $countfile="count.txt";
 if(!file_exists($countfile))
 {
 fopen($countfile,"w"); //如果此文件不存在，则自动建立一个
 }
 $fp=fopen($countfile,"r");
 $num=fgets($fp,20);
 $num=$num+1; //每次其值自动加一
 fclose($fp);
 $fp=fopen($countfile,"w");
 fwrite($fp,$num); //更新其值
 fclose($fp);
//利用上面自动计数的值获得HTML的路径$path
 $houzui=".php"; 
 $htmlfile ="archives";
 if (!is_dir($htmlfile)) //先判断是否已经创建了此目录！无，则先创建此目录
{
mkdir($htmlfile);
}
 $path=$htmlfile."/".$num.$houzui;
 //这样形成的路径是自动增长的，如1.html,2.html,3.html……添加一条新闻便自动加上1
 //以下用SQL语句添加数据至表 news
 $sql="insert into news (title,content,path) values (‘".$title."’,’".$content."’,’".$path."’)";
 $query=mysql_query($sql);
 //以下为关键之处，把从表单获得的数据替换模板中的{title},{content}标记
 $fp=fopen("model.php","r"); //只读打开模板
 $str=fread($fp,filesize("model.php"));//读取模板中内容
 $str=str_replace("{title}",$title,$str);
 $str=str_replace("{content}",$content,$str);//替换内容 
 fclose($fp); 
 $handle=fopen($path,"w"); //写入方式打开新闻路径
 fwrite($handle,$str); //把刚才替换的内容写进生成的HTML文件
 fclose($handle);
//收尾工作:
echo "查看刚才添加的新闻"; 
?>
```

add.php首先生成count文件，主要用来计数，以后每生成一个html，就加1.然后把生成的html文件路径，文件名称，内容存入数据库。之后最主要的是，使用模板生成html文件。模板中需要替换的地方使用{}留着标记。
