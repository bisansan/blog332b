---
title: Ubuntu  开机出现grub无法启动
tags: []
id: '794'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
date: 2019-08-14 11:42:31
---

方法一 使用命令修复试试

1.开机进入grub后，输出ls会出现下面内容，请自己用肉眼判断那个分区是你的启动分区，当然也可以通过ls (hd1,gpt1)/来查看分区包含的文件目录信息

```
grub>ls
(hd0,1),(hd0,5),(hd0,3),(hd0,2),(hd1,gpt1),(hd1,gpt2)
grub>ls (hd1,gpt1)/
/EFI,/BOOT
```

2.找到分区开始设置并启动分区

```
grub>set root=(hd1,gpt1)
grub>set prefix=(hd1,gpt1)/boot/grub
grub>normal 

# 输入上面命令 不会提示任何信息，如果错误请检测命令设置是否正确
```

3.进入系统后，更新grub

```
sudo update-grub

#不确定那个分区可以用 sudo fdisk -l查看
sudo grub-install /dev/sda

#第一条命令执行成功，第二条命令执行失败，英文提示为没有找到efi分区
```

方法二 使用boot repir修复

1.找到ubuntu官方镜像制作一个usb启动盘

2.制作完成后进入Live系统，保持系统联网，添加下面源，并安装boot repair

```
## 添加源
sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt-get update  

## 安装boot repir
sudo apt-get install -y boot-repair && boot-repair
```

3.不要直接点Recommended Repair，打开底部Advance options，选择正确的分区，再进行修复

我用此方法修复系统成功，方法一失败了，方法仅供参考，请多试