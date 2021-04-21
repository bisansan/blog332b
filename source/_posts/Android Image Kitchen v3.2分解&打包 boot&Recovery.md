---
title: Android Image Kitchen v3.2分解&打包 boot&Recovery
tags: []
id: '10'
categories:
  - - 其他分类
  - - 软件工具
date: 2018-03-24 04:14:00
---

客户端包含Windows Linux Android（REC卡刷）  
这里只讲一下在windows端的操作方法：

1）下载并解压缩附件（Android.Image.Kitchen.v1.8-Win32.zip）  
2）在CMD中使用命令：unpackimg ，或者可以拖放img到unpackimg.bat。 这将分解img并解压到ramdisk的一个子目录中。  
3）接下来你就可以XXOO ramdisk了，按你喜欢的姿势、方式去XXOO。  
4）上面XXOO完成后，直接点击repackimg.bat（repackimg.bat 这个批处理脚本不需要输入命令，只要点击运行）。可以直接打包成image-new.img文件。

5）最后支持cleanup.bat来清理文件夹并重置为初始状态，消除以下文件与文件夹：split\_img + ramdisk的目录和任何新的打包的ramdisk或img文件。

链接: [https://pan.baidu.com/s/1FC0l6zi3Je2bREhxFJhqQw](https://pan.baidu.com/s/1FC0l6zi3Je2bREhxFJhqQw) 密码: sww4  
![15887885545.png](http://post.332b.com/usr/uploads/2018/03/1090277441.png "15887885545.png")