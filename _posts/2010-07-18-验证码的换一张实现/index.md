---
title: "验证码的“换一张”实现"
date: 2010-07-18
categories: 
  - "website"
tags: 
  - "php"
---

突然有一天评论条数激增，还以为是流量大涨了呢，仔细一看是些垃圾评论，且评论的间隔极短，突破了JS的限制，可能是使用了评论工具实现的。

谷歌早有远见，在[用户生成的垃圾评论](http://www.google.com/support/webmasters/bin/answer.py?hl=cn&answer=81749)中总结了对抗垃圾评论的方法，同时提供了reCAPTCHA这个很强悍的工具，不过使用前需要注册。使用方法比较简单，和一般的验证码没有太大的区别，且Google给的使用说明足够详细。只是我考虑到这个家伙太过庞大，而且占用面积大，用在注册页面还算可以，如果用在评论验证就显得“大炮打蚊子”。

于是就使用个简单点的，放在附件里吧，这里主要说明的是“换一张”的实现，代码如下：

```
<input id="captcha-form" name="captcha" size="4" type="text" />
<img id="captcha" src="captcha.php" alt="" />
<a id="change-image" href="#">换一张</a>
```
