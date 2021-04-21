---
title: Ubuntu   不能播放html5视频的两种解决方法
tags: []
id: '823'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
abbrlink: 190be277
date: 2019-08-21 12:42:37
---

要看视频就会遇到这些问题，不知道是怎么回事，Ubuntu好像不能直接播放视频，需要安装插件，有下面两种方法可以解决

1.解决不能播放html5视频的方法

```
sudo apt-get install ubuntu-restricted-extras

# 一路默认回车键即可
```

2.安装adobe flash插件，不过Flash将于2020年停止更新，chrome浏览器也将于2020年不再支持flash插件

```
sudo apt-get install flashplugin-installer
```