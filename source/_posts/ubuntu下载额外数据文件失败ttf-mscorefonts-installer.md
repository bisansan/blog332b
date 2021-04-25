---
title: Ubuntu下载额外数据文件失败ttf-mscorefonts-installer
tags: [ubuntu,linux]
id: '685'
categories:
  - - 技术教程
abbrlink: d10ebb01
date: 2019-06-23 06:30:37
---

下载额外数据文件失败

以下软件包要求安装后下载附加数据，但其数据无法下载或无法处理。

ttf-mscorefonts-installer

稍后系统将自动重试下载，您也可以手工立即重试。执行此命令需要有活动的网络连接。

先下载下面文件解压，然后执行命令填入解压目录，不要下载wd97vwr32.exe文件

备用地址：[https://sourceforge.net/projects/corefonts/files/the%20fonts/final/](https://sourceforge.net/projects/corefonts/files/the%20fonts/final/)

[font字体](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/06/font.zip)[下载](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/06/font.zip)

`sudo dpkg-reconfigure ttf-mscorefonts-installer`