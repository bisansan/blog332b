---
title: 初级小白向bios添加cpu的辛酸史
tags: [bios,windows]
id: '911'
categories:
  - - 技术教程
abbrlink: a90e412e
date: 2020-02-14 17:34:10
---

我太难了，这么多教程看来看去，每个教程不是这里缺点东西，就是那里缺点东西，看来看去真的很闹心，所以我就想写个总结教程，不用找点东西找来找去

想修改bios，就得先准备工具

1.提取机器bios工具和驱动程序

ch341a编程器，淘宝有卖的，记得要买免拆架子

ch341a硬件驱动和提取软件，下面是下载链接

[http://www.downcc.com/soft/20312.html](http://www.downcc.com/soft/20312.html)

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200211181332.png)

2.bios修改工具UBU

官网：[https://www.win-raid.com/t154f16-Tool-Guide-News-quot-UEFI-BIOS-Updater-quot-UBU.html](https://www.win-raid.com/t154f16-Tool-Guide-News-quot-UEFI-BIOS-Updater-quot-UBU.html)

3.微码文件

微码数据库 Linux-Processor-Microcode-Data-File

[https://downloadcenter.intel.com/download/27591/Linux-Processor-Microcode-Data-File](https://downloadcenter.intel.com/download/27591/Linux-Processor-Microcode-Data-File)

先说下贴主的机器是hp 800 g1，支持intel四代处理器，主板为q87，bios备份后为16m，楼主想给机器用上魔改后的lga 1150 cpu，以及给bios加上nvem驱动，下面贴主就开动了

一、利用ch341提取机器的bios.bin，直接参考百度，大概步骤就是，

1.拆机先找到bios的flash芯片

2.用夹子夹住芯片

3.用对应的编程软件读取Biso，然后保存到桌面为bios.bin

二、下载cpu微码，并找出对应的cpu微码文件

1.下载cpu微码文件后解压后得到数据文件microcode.dat

2.microdecode.exe解压微码数据文件，解压后会得到很多文件，文件排序如下

文件名： cpu0001067a\_plat00000044\_ver00000a0b\_date20100928.bin

结构对照： cpu+CPUID+\_plat+Platform+\_ver+Version+\_date+Date+.bin

3.找出自己想添加cpu对应的微码文件

微软cpuid参考表：

[https://support.microsoft.com/zh-cn/help/4346084/kb4346084-intel-microcode-updates](https://support.microsoft.com/zh-cn/help/4346084/kb4346084-intel-microcode-updates)

参考微软官方的微码cpuid，得出我想添加的i7-4870hq的cpuid为40661 ,我就找到了对应的文件是cpu000**40661**\_plat00000032\_ver00000019\_date20180121.bin

三、准备好微码文件后，我们先将nvme模块添加到Bios，然后再添加微码

1.我们先将nvme按图片上的操作将nvme模块插入到bios中

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214170051-1024x882.png)

2.按图片检查nvme模块是否插入成功

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214170810-1024x587.png)

四、将微码文件添加Bios中，准备打卡UBU文件工具，我用的是1.76版本

1.打卡ubu工具选择这个

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214171404.png)

2.解压bios自带的所有微码

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214171542.png)

3.一般解压文件在当前软件目录/Extracted/Intel，我们打开后会看到一个或多个文件，他们全是都是微码文件，现在我们要把主板自带和需要添加的微码文件进行合并，合并后，再替换bios的微码库，就可以支持我们想要支持的cpu了，现在开动

我们先将准备好的微码文件和bios解压后文件放在一起，cmd进入当前目录，使用 copy /b 微码文件1 + 微码文件2 = 合并文件 来生成，例如，下面的命令

copy /b cpu\_file1.bin + cpu\_file3.bin + cpu\_file3.bin = done.bin

4.生成微码文件后，点击这里选择合并后的文件进行替换

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214172741.png)

5.替换完后，按0进入主菜单，再选择0 EXIT，再选择Rename to mod\_bios.bin，就会生成修改后的bios文件

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/02/20200214173054.png)

到这里，整个教程就完了，得到修改后的bios文件后，可以直接刷入机器使用