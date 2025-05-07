---
title: "PHP仿Google验证码"
date: 2010-07-12
categories: 
  - "website"
tags: 
  - "php"
---

源文件地址：http://code.google.com/p/cool-php-captcha/

文件下载下来，只需要resources、captcha.php、example-form.php这三个文件。resources是字体资源，captcha.php是验证码文件，这两个文件不需要修改，需要修改example-form.php文件。

接收表单的文件修改为：

```
<form method="post" action="post.php">
```

验证码填写的表单是：

```
<input type="text" name="captcha" id="captcha-form" />
```

需要在post.php文件中使用$\_POST\["captcha"\]来接收填写的内容，系统生成的验证码设置在session中的格式是：$\_SESSION\['captcha'\]，下面就是判断填写的验证码是否和系统生成的验证码相等。

```
if (!empty($_REQUEST['captcha'])) {
  if (empty($_SESSION['captcha']) || trim(strtolower($_REQUEST['captcha'])) != $_SESSION['captcha']) {
     echo "输入的验证码错误";
  } else {
     //验证码正确的操作
  }
  unset($_SESSION['captcha']);//不管输入的验证码是否正确，都应该进行验证码的注销 
}
```
