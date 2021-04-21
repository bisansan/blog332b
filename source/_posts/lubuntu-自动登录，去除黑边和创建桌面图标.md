---
title: lubuntu   自动登录，去除黑边和创建桌面图标
tags: []
id: '809'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
abbrlink: b42e815a
date: 2019-08-15 11:35:47
---

本系统版本为lubuntu 19.04，以下教程仅供参考

一、自动登录开关

修改文件/etc/sddm.conf就可以了

```
# 安装编辑器
sudo apt install gedit 

#打开文件
sudo gedit /etc/sddm.conf
```

打开/etc/sddm.conf会看到如下

```
#  lubuntu 19.04的配置
# sddm.conf文件
[Autologin]
Session=Lubuntu

# 设置自动登录用户名，删除本行就代表关闭自动登录
User=yourname



# lubuntu 18.04的配置
# sddm.conf文件

# Name of session file for autologin session (if empty try last logged in)
Session=lxqt.desktop

# Username for autologin session
User=yourname
```

二、除去输入法黑边框和黑块背景

![](https://post.332b.com/wp-content/uploads/2019/08/e03a5fff42e2cde863e50f04ef9b655e992807d2.png)

搜狗的皮肤严重依赖混成，可以用xcompmgr轻量级混成管理器来解决

```
sudo apt install xcompmgr

# 打开窗口阴影 / 半透明：

xcompmgr -cC

# 如果不喜欢阴影，可以将透明度设为 0（完全透明）：

xcompmgr -cC -o 0
```

一直放在命令行运行也不现实，你可以将它添加开机启动命令里面，就不用开这终端了

三、创建系统桌面快捷方式图标

点击左下角打开程序菜单，看到自己想要的程序，将它的图标拖动到桌面就可以，如果程序图标有感叹号，双击打开有提示是否执行，单机鼠标右键选择信任该执行文件，就不会弹提示，可以直接打开