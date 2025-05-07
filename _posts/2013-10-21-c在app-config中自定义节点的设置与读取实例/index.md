---
title: "C#在App.config中自定义节点的设置与读取实例"
date: 2013-10-21
categories: 
  - "software_programming"
tags: 
  - "c"
---

我们往往需要在App.config中自定义一些节来满足实际需要，而不依赖于App.config的appSettings，下面通过一个简单的实例来说明自定义配置节点的设置与读取（该实例抽取于FTP上传程序）。

在App.config配置文件中使用自定义配置，需要在configSections中添加一个section元素，并指定此section元素对应的名字和类型，然后再在configuration根节点下面添加此自定义配置节。

1、我们在App.config中添加如下的自定义节点（配置了一组相同类型的节点，用于上传文件目录，FTP服务器地址及登陆信息）：

```
<!--自定义节点：上传文件目录，FTP服务器地址及登陆信息-->
  <DZConfig>
    <AddressConfig>
      <FilePath>D:\ABC\1\</FilePath>
      <LogPath>D:\ABC\</LogPath>
      <uploadUrl>ftp://10.1.1.2</uploadUrl>
      <userName>user</userName>
      <passWord>1234</passWord>
    </AddressConfig>
    <AddressConfig>
      <FilePath>D:\ABC\2\</FilePath>
      <LogPath>D:\ABC\</LogPath>
      <uploadUrl>ftp://10.1.1.3</uploadUrl>
      <userName>user</userName>
      <passWord>1234</passWord>
    </AddressConfig>
    <AddressConfig>
      <FilePath>D:\ABC\3\</FilePath>
      <LogPath>D:\ABC\</LogPath>
      <uploadUrl>ftp://10.1.1.4</uploadUrl>
      <userName>user</userName>
      <passWord>1234</passWord>
    </AddressConfig>
  </DZConfig>
```

2、然后在App.config的configSections中添加section元素（section 元素将配置节处理程序与配置元素或节关联）（其中name为自定义节点的名称，type为自定义节点解析文件的命名空间和自定义节处理程序的类名）

```
<configSections>    
    <section name="DZConfig" type="FTP_SendServices.ConvertCfgSectionHandler,FTP_SendServices"/>
</configSections>
```

3、创建自定义配置节处理程序，节处理程序用来解释并处理 Web.config 文件特定部分中 XML 配置元素中定义的设置，并根据配置设置返回适当的配置对象。使用该配置对象，以对自定义配置元素进行读取和写入。新建名为DZConfig.cs的文件，代码如下：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Xml;
using System.Configuration;
using System.Collections;

namespace FTP_SendServices
{
    public class DZConfigSection
    {
        DZConfigSection() { }
        #region 属性定义

        private string _FilePath;
        private string _LogPath;
        private string _uploadUrl;
        private string _userName;
        private string _passWord;

        public string FilePath
        {
            get { return _FilePath; }
            set { _FilePath = value; }
        }

        public string LogPath
        {
            get { return _LogPath; }
            set { _LogPath = value; }
        }

        public string uploadUrl
        {
            get { return _uploadUrl; }
            set { _uploadUrl = value; }
        }

        public string userName
        {
            get { return _userName; }
            set { _userName = value; }
        }

        public string passWord
        {
            get { return _passWord; }
            set { _passWord = value; }
        }

        #endregion

        
        public DZConfigSection(XmlNode AddressConfig)
        {
            XmlElement c = (XmlElement)AddressConfig;
            _FilePath = c.SelectSingleNode("FilePath").InnerText;
            _LogPath = c.SelectSingleNode("LogPath").InnerText;
            _uploadUrl = c.SelectSingleNode("uploadUrl").InnerText;
            _userName = c.SelectSingleNode("userName").InnerText;
            _passWord = c.SelectSingleNode("passWord").InnerText;                     

        }

    }
    
    //创建一个实现 System.Configuration.IConfigurationSectionHandler 接口的公共类。
    public class ConvertCfgSectionHandler : IConfigurationSectionHandler
    {
        public ConvertCfgSectionHandler() { }
        public object Create(object parent, object configContext, XmlNode section)
        {
	    //添加您自己的代码，以执行所需的配置工作。
            List _list = new List();
            foreach (XmlNode AddressConfig in section.SelectNodes("//AddressConfig"))
            {
                DZConfigSection _DZConfig = new DZConfigSection(AddressConfig);
                _list.Add(_DZConfig);
            }
            return _list;            
            
        }
       
 
    }

    public class DZConfig
    {
     
        public static List GetConfigList()
        {
           
            return (List)ConfigurationSettings.GetConfig("DZConfig");
        }
    }
}
```

4、在程序中使用配置节点信息。下面就是节点的读取，遍历整个自定义节点的数据：

```
List _ConfigList = DZConfig.GetConfigList();
foreach (DZConfigSection Config in _ConfigList)
{
    LogPath  =Config.LogPath + "log" + DateTime.Now.ToString("yyyy-MM-dd") + ".txt";
    FileHelper.WriteFile(LogPath, DateTime.Now.ToString() + "　　　数据发送功能启动！");
    string dir = Config.FilePath;
    string uploadUrl =Config.uploadUrl;
    string userName = Config.userName;
    string passWord = Config.passWord; 
    string[] files = Directory.GetFiles(dir);
}
```
