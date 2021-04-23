---
title: lubuntu   挂机和休眠后黑屏无法启动
tags: [ubuntu,linux,xfce]
id: '827'
categories:
  - - 技术教程
abbrlink: d14dba64
date: 2019-08-21 15:22:21
---

原因很简单：xfce4默认锁屏挂了，我们无法打开界面，解决方法如下

```
sudo apt install gnome-screensaver

# 这个是gnome的锁屏，我们用它来替换xfce4的锁屏
```

然后在设置中找到会话启动，设置 =》会话和启动

![](https://post.332b.com/wp-content/uploads/2019/08/2019-08-21_15-16.png)

点击应用程序自启动，然后取消勾选Light locker，也就是锁屏锁，重启后就正常了

![](https://post.332b.com/wp-content/uploads/2019/08/2019-08-21_15-20.png)