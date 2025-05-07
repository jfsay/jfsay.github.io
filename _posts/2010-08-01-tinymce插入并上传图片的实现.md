---
title: "TinyMCE插入并上传图片的实现方法"
date: 2010-08-01
categories: 
  - "website"
tags: 
  - "tinymce"
---

TinyMCE自带的“插入图片”只能插入图片的链接（也就是外链），不能上传到网站服务器上，以前我的图片就是放在雅虎的Flickr!上的，想着放在别人的那里终归来说不太保险，于是想寻求一个在TinyMCE里就可以实现插入图片并上传到网站目录中的插件。

TinyMC官网上有个插件叫做MCFileManager，可以使用它来进行图片管理，无奈它是收费的。于是Google几十下，试了好几种方法总是有问题，几经周折找到了完美解决此问题的地方Simple Image Upload Plugin for TinyMCE，此网站提供一款及其简单并且免费开源的TinyMCE图片上传插件markettoimages. 配置和使用方法网站上说的简单明了，现摘录如下。

1\. Download distribution pack. Unzip it into TinyMCE’s **plugins** folder.（[下载](https://docs.google.com/leaf?id=0BylPy_4csyrXMzJiZDNjYjAtNmI1Ny00NzY5LWFlOWItNzI2OWUxMzc0ZDUz&sort=name&layout=list&num=50)markettoimages包，解压并存放在TinyMCE的plugins文件夹中。）

2\. Edit **config.php** file found in **plugins/markettoimages**. Minimally, you should only specify a target directory for your uploads. Every block of config. php is well-commented, so I think everything should go right.（编辑plugins/markettoimages中的config.php文件，指定上传图片文件的存放位置。具体的设置是把markettoimages/config.php的28行：$config\['img\_path'\] = '/images/somefolder';修改为自己需要的位置。提醒：路径是相对网站根目录的，没有最后的斜杠“/”。）

3\. Activate **markettoimages** plugin and add markettoimages button in TinyMCE. Don’t forget to set theme: advanced and realtive\_urls:false. See an exmple below:（激活markettoimages插件，并在TinyMCE中添加markettoimages按钮。不要忘记设置theme为advanced以及设置relative\_urls为false.下面是一个配置的例子，具体位置是在调用TinyMCE的初始化语句部分。）

```
tinyMCE.init({
    theme : "advanced",
    relative_urls : false,
    plugins : "markettoimages, ***",
    theme_advanced_buttons1 : "markettoimages,|,***"

    * * *
});
```
