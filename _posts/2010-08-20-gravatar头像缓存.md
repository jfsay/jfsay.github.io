---
title: "PHP实现Gravatar头像缓存"
date: 2010-08-20
categories: 
  - "website"
tags: 
  - "头像"
---

继留言加入Gravatar头像功能之后，在需要Gravatar头像的地方就会向Gravatar服务器发送请求并要求返回，这无疑会延缓网页的加载时间。通常的办法是把Gravatar头像缓存到本地服务器上，毕竟调用本地方便快捷。

这里我们只需要copy函数，把Gravatar头像copy到本机即可。一般的免费空间的copy会被关闭，可以通过下面的代码测试一下：

```
<?php 
echo copy("index.php","index123456.php");
?>
```

如果返回结果是1，并且在根目录下发现名为"index123456.php"的文件，说明copy是可以用的。

把上面的代码延伸成如下的代码（核心也就是copy函数，没有使用WP函数以及其他额外的函数，所以是通用的代码）：

```
<?php
function avatar($email,$size = '32',$default = '',$alt = 'gravatar'){ 
 $f = md5(strtolower($email)); 
 $a = 'avatar/'.$f.'.jpg'; 
 $e = 'avatar/'.$f.'.jpg'; 
 $t = 1209600; //设定14天 
 if (empty($default)) $default = 'avatar/default.jpg'; 
 if (!is_file($e) || (time() - filemtime($e)) > $t ){ //当头像不存在或者超过14天才更新 
 $r = 'X'; 
 $g = sprintf( "http://%d.gravatar.com", ( hexdec( $f{0} ) % 2 ) ). '/avatar/'. $f. '?s=64&d='. $default. '&r='. $r; 
 copy($g, $e); $a = $g;//新头像 copy 时, 取 gravatar 显示 
 } 
 if (filesize($e) < 500) copy($default, $e); 
 echo "<img title='{$alt}' alt='{$alt}' src='{$a}' class='gravatar' height='{$size}' width='{$size}' />"; 
}
// -- END ----------------------------------------
//测试一下 
$value="123@example.com";//注册的邮件地址
//调用代码
avatar( $value, $size = '40', $default = 'monsterid', $alt = 'gravatar');
?>
```

这样的话就把Gravatar头像copy到根目录下名为avatar的文件夹中了。

参考资料：快乐忆站 地址：http://thin.tk/AB
