---
title: UBuntu使用：常用的软件安装和下载
tags: []
id: '342'
categories:
  - - 技术分享
abbrlink: '36436006'
date: 2018-12-03 14:16:41
---

chrome浏览器 sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/ wget -q -O - https://dl.google.com/linux/linux\_signing\_key.pub sudo apt-key add - sudo apt-get update sudo apt-get install google-chrome-stable 安装搜狗输入法 官方参考文档https://pinyin.sogou.com/linux/help.php 安装flash插件 sudo apt-get install flashplugin-installer Chrome浏览器设置代理 google-chrome --proxy-server="socks5://localhost:1080" VirtualBox遇到UUID重复问题，例如虚拟硬盘vdi复制会出现类似问题 **winodws命令：VBoxManage internalcommands sethduuid "E:\\VirtualBox VMs\\XP.vdi"** ubuntu命令：VirtualBox nternalcommands sethduuid /media/wng/Uz/win7/win732.vdi WPS字体缺失解决办法 [wps\_symbol\_fonts](https://post.332b.com/wp-content/uploads/2018/12/wps_symbol_fonts.zip) 国外下载地址：https://www.dropbox.com/s/lfy4hvq95ilwyw5/wps\_symbol\_fonts.zip

下载完成后，解压并进入目录中，继续执行： sudo cp \* /usr/share/fonts 执行以下命令,生成字体的索引信息： sudo mkfontscale sudo mkfontdir 运行fc-cache命令更新字体缓存。重启wps sudo fc-cache

wordpress摘要调整   iwata\_custom\_excerpt\_length( $length )

32weiku    sudo apt install lib32z1 lib32ncurses-dev

http://anduin.linuxfromscratch.org/sources/linux-firmware/amdgpu/

https://github.com/GPUOpen-Drivers/AMDVLK

https://people.freedesktop.org/~agd5f/radeon\_ucode/