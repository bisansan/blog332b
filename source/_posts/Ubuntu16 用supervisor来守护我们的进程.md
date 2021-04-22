---
title: Ubuntu16 用supervisor来守护我们的进程
tags: []
id: '14'
categories:
  - - 主机系统
    - ubuntu
  - - 技术分享
abbrlink: 22d4e5c9
date: 2018-03-31 09:54:00
---

Ubuntu16的后台进程如果经常出现挂掉，那就让supervisor守护它吧,本篇文章是用最高权限root来执行，其他用户登陆请自己切换root或者在前面加上sudo 1.习惯性先更新源，再安装supervisor

```
apt update & apt install supervisor
```

2.安装后并没有随开机自启，手动设置自动自启

```
systemctl enable supervisor 
```

3.下载我们的要后台执行的文件，并给权限

```
wget http://xxxx.com/ 
chomd 777 xxx  
```

4.supervisor的守护进程在ubuntu默认是写成一个独立的配置文件，supervisor 的进程文件一般是放在 /etc/supervisor/conf.d/ 目录下，例如创建一个test.conf 进程配置文件。

```
[program:test]           ###program 为要运行的进程的名称###
command=php artisan queue:work         ###command 为要执行的命令###
directory=/var/www/html/wisdom         ###directory 要执行命令的目录###
user=root                              ###user 运行的用户###
```

5.supervisor常见的管理命令

```
supervisorctl reload           ###重启supervisor,让配置文件生效###
supervisorctl startrestartstop  test       ###启动重启停止指定进程###
```

相关的一些常用命令 1.防火墙的禁用和启动 `ufw disableenable` 2.卸载iptables命令 `apt-get remove iptables` 3.关闭防火墙的其余命令

```
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
```

4.查看端口占用情况的命令 查看已经连接的服务端口（ESTABLISHED）

```
netstat -a
```

查看所有的服务端口（LISTEN，ESTABLISHED）

```
netstat -ap
```

查看指定端口，可以结合grep命令：

```
netstat -ap  grep 8080
```