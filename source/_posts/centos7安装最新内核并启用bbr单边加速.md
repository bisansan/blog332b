---
title: Centos7安装最新内核并启用BBR单边加速
tags: [centos,linux]
id: '218'
categories:
  - - 系统运维
abbrlink: 9c5d6626
date: 2018-10-28 15:23:45
---

1.安装第三方YUM仓库 `rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org` `rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm` 2.搜索最新的系统内核并安装 `yum --disablerepo="*" --enablerepo="elrepo-kernel" list available` `yum --enablerepo=elrepo-kernel install kernel-ml` 3.生成新的启动文件，打开/etc/default/grub找到`GRUB_DEFAULT=save`修改为`GRUB_DEFAULT=0` `grub2-mkconfig -o /boot/grub2/grub.cfg` 4.重新启动vps输入`uname -a`即可看到最新内核，修改系统变量 `echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf` 5.保存新规则并使其生效后，查看启动情况 `sysctl -p` `sysctl net.ipv4.tcp_available_congestion_control` 如果出现net.ipv4.tcp\_available\_congestion\_control = reno cubic bbr，只要有bbr就算成功 6.查看端口是否启动成功 `lsmod grep bbr` 成功就会显示tcp\_bbr               20480 6 7.默认启动内核修改方法 #1.查看启动项 `cat /boot/grub2/grub.cfg grep kernel-3.10.0-229` #1. 设置默认启动项 `grub2-set-default "kernel-3.10.0-229"` #3. 查看默认启动项 `grub2-editenv list` #4. 生成配置 `grub2-mkconfig -o /boot/grub2/grub.cfg` #备注： 在生成grub.cfg之前，最好先备份原始的grub.cfg文件 重新安装内核即可 yum -y update