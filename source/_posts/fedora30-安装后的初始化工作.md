---
title: fedora30 安装后的初始化工作
tags: []
id: '864'
categories:
  - - uncategorized
abbrlink: 1c7081be
date: 2019-09-30 12:33:11
---

fedora30 安装后的初始化工作

所有软件更新到最新的版本

```
sudo dnf update
```

安装完整内核工具

```
sudo yum install kernel-headers kernel-devel
```

安装中文输入法

```
# 安装输入法切换工具
sudo dnf install im-chooser
# 安装 fcitx
sudo dnf install fcitx
# 如果这一行无法执行，可以换成kde-config-fcitx
sudo dnf install kcm-fcitx
# 安装sunpinyin
sudo dnf install fcitx-sunpinyin
```

如果要安装第三方下面下来的rpm包，同时又有依赖如果解决，可以用下面命令，自动安装依赖

```
sudo yum -y localinstall *.rpm
```

安装 virtualbox无法启动，可能是没有执行下面命令

```
sudo /sbin/vboxconfig

# [witt@localhost ~]$ sudo  /sbin/vboxconfig
# vboxdrv.sh: Stopping VirtualBox services.
# vboxdrv.sh: Starting VirtualBox services.
# vboxdrv.sh: Building VirtualBox kernel modules.
```