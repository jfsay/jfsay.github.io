---
title: "记住帐号、记住密码、记住表单信息等“记住”的实现"
date: 2010-06-24
categories: 
  - "website"
tags: 
  - "php"
---

登录界面有记住帐号、记住密码，留言时有记住表单信息等，这使得用户在下次访问该页面时不用重复地输入重复的信息，减少重复劳动。网页设计者当然要满足用户的需求，那么PHP是怎么实现这些“记住”的呢。  
使用客户端的cookie可以实现上述需求，下面以留言板为实例来讲解：  
先看一下一般的Form（不具有记住功能的表单）：

```
<form action="post.php">
<p><input type="text" name="inpName" id="inpName"  /> <label for="inpName">名称(*)</label></p>
<p><input type="text" name="inpEmail" id="inpEmail" /> <label for="inpEmail">邮箱</label></p>
<p><input type="text" name="inpHomePage" id="inpHomePage" /> <label for="inpHomePage">网站链接</label></p>
<p><input name="btnSumbit" type="submit" tabcomment="6" value="提交"  /></p>
</form>
```

我们需要在名称、邮箱、网站链接处填上用户的信息，这些信息应该从用户上一次提交时得到。  
只需要在post.php中加入下面的语句：

```
$sql = "insert into comment (nid,username,email,info,ip,site,submit_time) values ('$nid','$username','$email','$info','$ip','$site',NOW())";
$result = mysql_query($sql);
setcookie("CookieNAME",mysql_insert_id(),time()+94608000,"/"); /* 三年后 cookie 才会失效 */
```

把刚添加进数据库中的记录id保存在CookieNAME中，保存时间为三年。  
上面是写入cookie，取出直接用$CookieNAME。可是取出id没什么用，我们需要的是用户的信息，那么就执行一下数据库查询操作就行了：

```
if(!empty($CookieNAME)){
$sql = "select username,email,site from comment where id=$CookieNAME";
$rss = mysql_query($sql);
$rs= mysql_fetch_array($rss);
}
```

然后把这些得到的信息填到上面的form表单中就完成了“记住”。  
可是用户不一定都希望被“记住”，那么就要增加一个复选框供用户选择。表单中在按钮的右边添加：

```

<input type="checkbox" name="chkRemember" value="1" id="chkRemember" />
<label for="chkRemember">记住我,下次回复时不用重新输入个人信息</label>
```

post.php处理时只需要简单的判断复选框有没有被选中即可：

```
if(!empty($_POST["chkRemember"])){//如果复选框选中，设置cookie
setcookie("CookieNAME",mysql_insert_id(),time()+94608000,"/"); /* 三年后 cookie 才会失效 */
}
```

整个过程就是这样的，登录框和这个实现起来差不多。
