---
title: Deepin安装最新版的火狐、chrome浏览器和Sublime text3
tags: [deepin,linux,chrome,Sublimetext]
id: '448'
categories:
  - - 技术教程
abbrlink: 5c87015e
date: 2019-01-09 17:58:35
---

火狐浏览器：可以在[https://pkgs.org/](https://pkgs.org/)搜索Firefox，选择ubuntu16.04安装就可以

dpkg -i http://archive.ubuntu.com/ubuntu/pool/main/f/firefox/firefox\_64.0+build3-0ubuntu0.16.04.1\_amd64.deb

火狐浏览器汉化，安装对应的中文包就可以了，下面网址用火狐打开哦 所有语言：https://addons.mozilla.org/zh-CN/firefox/language-tools/ 中文语言包：[https://addons.mozilla.org/zh-CN/firefox/addon/chinese-simplified-zh-cn-la/](https://addons.mozilla.org/zh-CN/firefox/addon/chinese-simplified-zh-cn-la/) 谷歌浏览器：最新版直接运行下面命令就可以了 dpkg -i https://dl.google.com/linux/direct/google-chrome-stable\_current\_amd64.deb Sublime text3安装： dpkg - i http://download.sublimetext.com/files/sublime-text\_build-3176\_amd64.deb 下载最新版方法：http://download.sublimetext.com/files/sublime-text\_build-版本号\_amd64.deb 汉化和插件还有激活办法请自行百度，下面解决中文输入问题 克隆这个git仓库

```
git clone https://github.com/Firef0x/SublimeText-i18n-zh.git
```

或者直接下载[foo.zip](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/foo.zip) 然后解压后给执行权限执行目录里的 chmod 777 sublime-imfix && ./sublime-imfix