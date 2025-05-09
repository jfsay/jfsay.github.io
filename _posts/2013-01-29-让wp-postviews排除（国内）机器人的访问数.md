---
title: "让WP-PostViews排除（国内）机器人的访问�?
date: 2013-01-29
categories: 
  - "website"
tags: 
  - "wp-postviews"
  - "排除"
  - "机器�?
  - "爬虫"
  - "蜘蛛"
  - "访问�?
---

博客[安装](http://www.jfsay.com/archives/690.html "iNove主题添加文章浏览次数的功�?)了WP-PostViews插件用来显示文章的浏览次数，但是我发现显示出来的访问次数与谷歌分析（Analytics）的统计数据不一致，WP-PostViews统计出来的数据远远大于谷歌分析的数据。于是我就怀疑WP-PostViews统计数据包含了机器人的访问量，可是我在插件的设置里面明明�?*Exclude Bot Views的值置为Yes**了，原则上已经排除了网络爬虫机器人的访问次数了�?
我在谷歌中满世界寻找WP-PostViews插件排除机器人访问的方法，来回变换中英文的搜索关键字，最终还是没有找到解决的办法。后来我才知道，国外用户使用WP-PostViews插件不会遇到我们的问题，原来从中做怪的是国内的机器人\\爬虫\\蜘蛛�?
求人不如求己，拿出[WP-PostViews插件](https://www.jfsay.com/archives/425.html "WP-PostViews插件的函数功能（包含浏览总数�?)的源代码来看。在wp-postviews.php找到了排除机器人访问次数的代码（不妨叫作Exclude Bot Views code），如下所示：

```
if(intval($views_options['exclude_bots']) == 1) {
	$bots = array('Google Bot' => 'googlebot', 'Google Bot' => 'google', 'MSN' => 'msnbot', 'Alex' => 'ia_archiver', 'Lycos' => 'lycos', 'Ask Jeeves' => 'jeeves', 'Altavista' => 'scooter', 'AllTheWeb' => 'fast-webcrawler', 'Inktomi' => 'slurp@inktomi', 'Turnitin.com' => 'turnitinbot', 'Technorati' => 'technorati', 'Yahoo' => 'yahoo', 'Findexa' => 'findexa', 'NextLinks' => 'findlinks', 'Gais' => 'gaisbo', 'WiseNut' => 'zyborg', 'WhoisSource' => 'surveybot', 'Bloglines' => 'bloglines', 'BlogSearch' => 'blogsearch', 'PubSub' => 'pubsub', 'Syndic8' => 'syndic8', 'RadioUserland' => 'userland', 'Gigabot' => 'gigabot', 'Become.com' => 'become.com');
	$useragent = $_SERVER['HTTP_USER_AGENT'];
	foreach ($bots as $name => $lookfor) { 
		if (stristr($useragent, $lookfor) !== false) { 
			$should_count = false;
			break;
		} 
	}
}
```

稍微解释一下上面的代码功能�?
$bots数组用来存放机器人标识的关键字�?
$useragent是访问站点的user-agent标识�?
foreach()用来遍历数组，如果探测到访问站点的user-agent标识和bots数组中机器人标识匹配，则不计数�?
作者想要实现排除机器人访问数的意图，通过以上的代码大致可以做到。但是仔细研�?bots数组会发现，它里面没有国内搜索爬虫的标识，比如Baiduspider�?60spider、Sosospider等。所以WP-PostViews插件并没有排除掉国内常见的机器人�?
我在站点统计中找到了站点的访问情况，一般的主机空间都会提供站点的Report功能。下图所示为我的站点一周内的访问情况：

![Agent](/images/8426015982_69cd6315d7_z.jpg)

可以看到站点每天被不同的蜘蛛或机器人访问，而这些机器人并没有记录在WP-PostViews插件的bots数组中，以至于并没有被排除掉。为了排除掉国内的蜘蛛访问数，只需在bots数组中把蜘蛛的标识添加进去即可。我也是懒于研究了，干脆来个干净的，把Spider、Bot、Slurp统统咔嚓掉（注意：这种做法有误杀的可能）。具体做法是修改Exclude Bot Views code为下面的代码�?
```
if(intval($views_options['exclude_bots']) == 1) {
	$bots = array('Google Bot' => 'googlebot', 'Google Bot' => 'google', 'MSN' => 'msnbot', 'Alex' => 'ia_archiver', 'Lycos' => 'lycos', 'Ask Jeeves' => 'jeeves', 'Altavista' => 'scooter', 'AllTheWeb' => 'fast-webcrawler', 'Inktomi' => 'slurp@inktomi', 'Turnitin.com' => 'turnitinbot', 'Technorati' => 'technorati', 'Yahoo' => 'yahoo', 'Findexa' => 'findexa', 'NextLinks' => 'findlinks', 'Gais' => 'gaisbo', 'WiseNut' => 'zyborg', 'WhoisSource' => 'surveybot', 'Bloglines' => 'bloglines', 'BlogSearch' => 'blogsearch', 'PubSub' => 'pubsub', 'Syndic8' => 'syndic8', 'RadioUserland' => 'userland', 'Gigabot' => 'gigabot', 'Become.com' => 'become.com',  'Feedburner' => 'feedburner', 'Spider' => 'spider', 'Bot' => 'bot', 'Slurp' => 'slurp');
	$useragent = $_SERVER['HTTP_USER_AGENT'];
	foreach ($bots as $name => $lookfor) { 
		if (stristr($useragent, $lookfor) !== false) { 
			$should_count = false;
			break;
		} 
	}
}
```
