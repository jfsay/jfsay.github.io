---
title: "Python循环解析文件夹下XML文件，并将结果插入到SQLServer数据库"
date: 2018-04-20
categories: 
  - "software_programming"
tags: 
  - "python"
---

需求如下：A、B两台服务器分别在内外网，B服务器取A服务器上数据库中的数据，需要通过XML报文传输数据，A服务器生成XML报文，B服务器拿到XML报文解析入库。

需求分析：

A服务器发送过来的XML报文源源不断地放到B服务器上的以下目录：D:\\test中

- 1、程序遍历test目录，得到目录中所有XML文件路径

- 2、解析XML文件

- 3、将解析结果插入SQLServer数据库

以上三步的实现参见以下三篇文章：

[Python遍历文件夹中文件操作](http://www.jfsay.com/archives/1416.html)、[Python使用XPath解析XML文档](http://www.jfsay.com/archives/1414.html)****、****[Python使用pymssql连接SQLServer数据库](http://www.jfsay.com/archives/1415.html)

只需把三步串起来就能实现需求了，额外增加以下内容：

- 1、解析完一个XML文件，需要把它从目录中移走（备份）

- 2、程序常驻内存，永远在执行，不退出，增加休眠时间

完整的代码如下：

```
import os,shutil
from lxml import etree
import pymssql
from datetime import datetime
import time

rootdir = 'D:/test'
def mssql(sql):
    conn=pymssql.connect(host='.',user='sa',password='test',database='test')
    '''
    如果和本机数据库交互，只需修改链接字符串
    conn=pymssql.connect(host='.',database='Michael')
    '''
    cur=conn.cursor()    
    cur.execute(sql)
    conn.commit()    
    cur.close()
    conn.close()

def ReadXML(path):
    tree = etree.parse(path)
    root = tree.getroot()
    for child in root:
        try:
            NO=child.xpath('./NO/text()')[0]
            STEP_CODE=child.xpath('./STEP_CODE/text()')[0]
            MARK=child.xpath('./MARK/text()')[0]
            INSERT_DATE=datetime.now().strftime('%Y-%m-%d %H:%M:%S')
        except Exception as e:  
            print(e,"XML读取失败")
        try:
            sql="insert into HEAD VALUES('"+NO +"','"+STEP_CODE+"','"+MARK+"',''"+INSERT_DATE+"')"
            #插入数据库            
            mssql(sql)  
        except Exception as e:  
            print(e,"数据插入失败")
    dstfile=rootdir+"/bak/"#备份目录
    try:
        shutil.move(path,dstfile)#移动文件 
    except Exception as e:
        print(e)   

def main():    
    #列出文件夹下所有的目录与文件
    l = os.listdir(rootdir)     
    for i in range(len(l)):
            path = os.path.join(rootdir,l[i])
            if os.path.isfile(path):
                   path=path.replace("\\", "/")                   
                   ReadXML(path)

if __name__=="__main__":
    while True:
        main()
        print("开始抓取")
        time.sleep(15)#休眠15秒
```
