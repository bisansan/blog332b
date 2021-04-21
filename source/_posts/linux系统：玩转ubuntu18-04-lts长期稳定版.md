---
title: linux系统：玩转ubuntu18.04 LTS长期稳定版(一)
tags: []
id: '518'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
abbrlink: f1958246
date: 2019-01-30 17:15:56
---

ubuntu版本：18.04 linux内核：4.15自带内核，不建议自己手动升级内核，有些软件就基于这个内核，跟着官方走就行了   一.美化gnome桌面 `sudo apt install gnome-tweak-tool`   #中文名优化，一个高级扩展管理器`sudo apt-get install gnome-shell-extension-top-icons-plus gnome-tweaks`          ###开启程序托盘 软件商店搜索 Dynamic Top Bar     ##顶部状态栏透明插件 Dash to dock       ##自定义左侧状态栏 这个是在线安装插件https://extensions.gnome.org/，不过一般作为备用，要安装直接在商店搜索插件就可以了 在文件管理器主目录，Ctrl + H可以显示隐藏文件，就可以看到.local .local/share中新建themes、fonts、icons 三个文件夹，分别存放主题、字体和图标 。 windows或者mac风格主题桌面美化：[https://github.com/vmavromatis/gnome-layout-manager](https://github.com/vmavromatis/gnome-layout-manager)     二.拼音输入法 安装ibus-sunpinyin 为什么要安装sunpinyin，因为gnome桌面集成了ibus，所以使用fcitx兼容性不好，我不想折腾，而且这个输入法也够用 [https://launchpad.net/ubuntu/trusty/amd64/python-ibus/1.5.5-1ubuntu3.2](https://launchpad.net/ubuntu/trusty/amd64/python-ibus/1.5.5-1ubuntu3.2) 安装输入法 `apt install ibus-sunpinyin python-ibus libcanberra-gtk-module` 安装这个插件，避免有些设置界面打不开 `/usr/lib/ibus/ibus-setup-sunpinyin`   #打开输入法设置界面   安装fcitx-sogoupinyin搜狗输入法，也可以配合ibus输入法一起使用 官网：[https://pinyin.sogou.com/linux/](https://pinyin.sogou.com/linux/) `wget  http://cdn2.ime.sogou.com/dl/index/1524572264/sogoupinyin_2.2.0.0108_amd64.deb?st=zUT1RU19mmznZaP98biXwg&e=1548990251&fn=sogoupinyin_2.2.0.0108_amd64.deb` `sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb` `sudo apt -f install`       三、安装chrome浏览器 `sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/` `wget -q -O - https://dl.google.com/linux/linux_signing_key.pub sudo apt-key add -` `apt update` `sudo apt-get install google-chrome-stable`     四、安装flash player插件使用 `sudo apt-get install flashplugin-installer`     五、安装linux版本迅雷Uget `sudo apt install uget aria2`     六、安装office办公WPS软件 官网下载最新安装包 [http://www.wps.cn/product/wpslinux](http://www.wps.cn/product/wpslinux) 解决WPS字体问题：[wps\_symbol\_fonts.zip](https://post.332b.com/wp-content/uploads/2018/12/wps_symbol_fonts.zip) 1.自己下载字体压缩包，手动点击逐个安装 2.命令行安装，需要下载字体包

下载完成后，解压并进入目录中，继续执行： `sudo cp * /usr/share/fonts` 执行以下命令,生成字体的索引信息： `sudo mkfontscale` `sudo mkfontdir` 运行fc-cache命令更新字体缓存。重启wps `sudo fc-cache`

下载最新包安装，下面做个示例 `wget http://kdl.cc.ksosoft.com/wps-community/download/6757/wps-office_10.1.0.6757_amd64.deb` `dpkg -i wps-office_10.1.0.6757_amd64.deb` `sudo apt -f install`     七、安装网易云音乐 官网：[https://music.163.com/#/download](https://music.163.com/#/download) `wget http://d1.music.126.net/dmusic/netease-cloud-music_1.1.0_amd64_ubuntu.deb` `sudo dpkg -i netease-cloud-music_1.1.0_amd64_ubuntu.deb` `sudo apt -f install` 解决无法直接点击打开，需要root权限或在`sudo netease-cloud-music` 才能打开 原文：https://blog.csdn.net/Handoking/article/details/81026651 `sudo gedit /etc/sudoers` 添加`YOURNAME ALL = NOPASSWD: /usr/bin/netease-cloud-music`到最后一行，YOURNAME为你的用户名，注意大小写 `sudo gedit /usr/share/applications/netease-cloud-music.desktop` 将Exec修改为`Exec=sudo netease-cloud-music %U` 已知问题：无法在输入框输入中文，可以在其他地方输入中文，然后复制粘贴    

八、Sublime text3安装： `wget http://download.sublimetext.com/files/sublime-text_build-3176_amd64.deb` `dpkg –i sublime-text_build-3176_amd64.deb` 下载最新版方法：http://download.sublimetext.com/files/sublime-text\_build-版本号\_amd64.deb 汉化和插件还有激活办法请自行百度，下面解决中文输入问题 克隆这个git仓库

```
git clone https://github.com/Firef0x/SublimeText-i18n-zh.git
```

或者直接下载[foo.zip](https://post.332b.com/wp-content/uploads/2019/01/foo.zip) 然后解压后给执行权限执行目录里的 `chmod 777 sublime-imfix && ./sublime-imfix`

汉化包[LocalizedMenu-master.zip](https://post.332b.com/wp-content/uploads/2019/01/LocalizedMenu-master.zip)：https://github.com/zam1024t/LocalizedMenu

复制到：`/home/user/.config/sublime-text-3/Packages` ，其中user为你的用户名

控制面板插件[Package Control.zip](https://post.332b.com/wp-content/uploads/2019/01/Package-Control.zip)，复制到下面的目录即可

/opt/sublime\_text/Packages

      九、安装数据库图形界面管理工具mysql workbench（**非中文软件**）

默认安装目录：/usr/lib/mysql-workbench

官网：https://dev.mysql.com/downloads/workbench/

```
wget https://cdn.mysql.com//Downloads/MySQLGUITools/mysql-workbench-community_8.0.14-1ubuntu18.04_amd64.deb
```