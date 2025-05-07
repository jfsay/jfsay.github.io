---
title: "WP-Flickr插件显示640图片尺寸大小的修改"
date: 2011-11-12
categories: 
  - "website"
tags: 
  - "flickr"
  - "wordpress"
  - "wp-flickr"
  - "插件"
---

上传到Flickr上的每张照片，一般都会自动生成如下几种大小像素的图片，每张照片的连接地址其实是有规则的。

**1、s表示一个宽度为75高度也为75的“正方形图”**

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9\_s.jpg

![](images/6249268041_4dcc8047b9_s.jpg)

**2、t表示一个宽度为100高度等比的“缩图”**

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9\_t.jpg

![](images/6249268041_4dcc8047b9_t.jpg)

**3、m表示一个宽度为240高度等比的“小图”**

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9\_m.jpg

![](images/6249268041_4dcc8047b9_m.jpg)

**4、为空的表示一个宽度为500高度等比”中型图”**

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9.jpg

![](images/6249268041_4dcc8047b9.jpg)

**5、z表示一个宽度为640高度等比的“中型图”**

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9\_z.jpg

![海边](images/6249268041_4dcc8047b9_z.jpg)

**6、b表示一个宽度为1024高度768的“大图”** (这里图片太大，省略显示)

https://farm7.staticflickr.com/6162/6249268041\_4dcc8047b9\_b.jpg

上述6种不同大小的图片地址的不同之处是.jpg之前的字母，也就是说，我们可以通过修改这些字母得到不同大小尺寸的图片。

我目前使用的Flickr插件是**WP-Flickr**，它可以方便快捷地插入Flickr中的图片大到编辑的文章中，不足之处是，不支持640尺寸的图片。而我的博客中使用的图片大多是640大小的，很少使用1024大小的。

所以我干脆替换掉1024的图片设置为640的，具体做法是：

**1、wp-flickr/wp-flickr-write.php**

```
<option value=”_b” <?php if ($wpflickr_config[‘photo_size’] == “b”) echo “selected”; ?>>Large (1024 x 768 pixels)</option>
```

替换为：

```
<option value=”_z” <?php if ($wpflickr_config[‘photo_size’] == “z”) echo “selected”; ?>>Large (640 x359 pixels)</option>
```

**2、wp-flickr/wp-flickr-admin.php**

```
<option value=”b” <?php if($wpflickr_config[‘photo_size’] == “b”) echo “selected”; ?>>Large (1024 x 768 pixels)</option>
```

替换为：

```
<option value=”z” <?php if($wpflickr_config[‘photo_size’] == “z”) echo “selected”; ?>>Large (640 x 359 pixels)</option>
```
