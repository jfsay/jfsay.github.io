---
title: "Python+selenium自动签到完整步骤"
date: 2019-07-31
categories: 
  - "software_programming"
tags: 
  - "python"
---

1、安装Python（加入环境变量）  
2、测试Python是否安装成功：cmd - python  
3、下载selenium  
4、安装selenium：cmd到selenium的目录，python setup.py install  
5、下载urllib3  
6、安装urllib3: cmd到selenium的目录，python setup.py install  
7、下载Chrome浏览器对应的驱动chromedriver.exe  
8、将chromedriver.exe复制到python安装目录Scripts目录下

代码如下：

```
from bs4 import BeautifulSoup 
from selenium import webdriver 
import requests 
import time

option = webdriver.ChromeOptions()
option.add_argument('disable-infobars') #解决Chrome提示被自动程序控制

browser = webdriver.Chrome(chrome_options=option) 
	
browser.get('http://xxxx/')

browser.find_element_by_xpath('//*[@id="signInName"]').send_keys('xxxx')
	
browser.find_element_by_xpath('//*[@id="password"]').send_keys('xxxx')

browser.find_element_by_xpath('//*[@id="SignInButton"]').click()	

time.sleep(10)

browser.find_element_by_xpath('/html/body/div/ul/li[1]').click()

time.sleep(10)

browser.find_element_by_xpath('//*[@id="123456"]').click()

time.sleep(10)

browser.quit();
```

其他：

1、找Xpath的偷懒方法：在页面选中某一元素，在F12的开发工具内，点击对应元素的右键copy—>xpath即可取到某元素的xpath

2、在Chrome所有页面启用flash的方法，将下面代码保存为.reg文件，双击运行。

```
Windows Registry Editor Version 5.00  
 
[HKEY_CURRENT_USER\SOFTWARE\Policies\Chromium] 
"AllowOutdatedPlugins"=dword:00000001 
"RunAllFlashInAllowMode"=dword:00000001 
"DefaultPluginsSetting"=dword:00000001 
"HardwareAccelerationModeEnabled"=dword:00000001 
 
[HKEY_CURRENT_USER\SOFTWARE\Policies\Chromium\PluginsAllowedForUrls] 
"1"="https://*" 
"2"="http://*" 
 
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome] 
"AllowOutdatedPlugins"=dword:00000001 
"RunAllFlashInAllowMode"=dword:00000001 
"DefaultPluginsSetting"=dword:00000001 
"HardwareAccelerationModeEnabled"=dword:00000001 
 
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\PluginsAllowedForUrls] 
"1"="https://*" 
"2"="http://*"
```
