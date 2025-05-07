---
title: "卸载手机自带的系统应用（免root）"
date: 2020-04-30
categories: 
  - "software_programming"
tags: 
  - "root"
  - "手机"
---

手机root后会出现发热、耗电大、无法OTG升级等问题，我现在基本上不会root手机了。但是自带的系统应用没法删除，还在后台跑占内存又耗电，很烦人。现在发现可以通过adb删除系统应用，这回当下搬运工，记录下操作的步骤：

1. 用数据线将手机和PC连接
2. 打开开发者选项中的USB调式
3. 下载adb  https://developer.android.google.cn/studio/releases/platform-tools.html
4. 将下载好的解压包解压，进入platform-tools文件夹，在文件夹空白区域右键shift+鼠标右键，点击“点此打开命令窗口”
5. 输入"adb devices"看是否成功

连接成功以后就可以通过命令对手机进行操作了。

☆ adb 卸载app的命令是格式是：adb shell pm uninstall --user 0 APP包名

☆ adb 禁用app的命令是格式是： adb shell pm disable-user APP包名

注：我这边试了卸载“系统更新”APP失败，禁用的话就成功了。

_附魅族系统APP包名_

新闻资讯 com.meizu.media.reader

魅族视频 com.meizu.media.video (不建议卸载，卸载了通过图库无法播放录像)

魅族音乐 com.meizu.media.music

换机助手 com.meizu.datamigration

生活助手 com.meizu.media.life

钱包 com.meizu.flyme.wallet(不建议卸载)

游戏中心 com.meizu.flyme.gamecenter

福利中心 com.meizu.compaign

系统更新 com.meizu.flyme.update(不建议卸载)

魅族计步器 com.meizu.net.pedometer

魅族语音 com.meizu.voiceassistant

魅族游戏框架 com.meizu.gamecenter.service(不建议卸载)

读书 com.meizu.media.ebook

趣视频 com.flyme.videoclips

魅族服务 com.meizu.mcare

魅族游览器 com.android.browser（不建议卸载）

邮件 com.android.email

用户帮助 com.meizu.feedback

搜索 com.meizu.net.search

地图 com.meizu.net.map

应用商店 com.meizu.mstore（不建议卸载）

天气 com.meizu.flyme.weather

搜狗输入法 com.sohu.inputmethod.sogou

查看已安装APP，adb shell pm list package
