---
title: Centos6.5系统yum安装apache2.4并配置目录浏览访问
tags: []
id: '158'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - 其他Linux系统
  - - 技术分享
date: 2018-10-20 21:15:32
---

第一步、安装第三方仓库，本地apache最新版为2.2.15，第三方为2.4.27 `yum install centos-release-scl` `rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm` 第二步、检查并安装的apache2.4 `yum search httpd24`     ##列出所有跟http2.4相关并可以安装的包 `yum install httpd24-httpd`   ##安装最新apache2.4 第三步、设置开机自动启动和开始服务 `chkconfig httpd24-httpd on`    ##设置开机启动 `service httpd24-httpd start`    ##启动apache 第四步、检查httpd是否启动，没有启动不显示任何东西，启动会显示tcp 0 0 0.0.0.0:80 0.0.0.0:\* LISTEN 1350/httpd `netstat -lnpgrep 80`   ##检查httpd是否启动 第五步、查找配置文件目录 `rpm -ql httpd24-httpd`   ##查找软件安装位置 `cd /opt/rh/httpd24/root/etc/httpd/conf.d`    ##进入配置目录 第六步、找到welcome.conf查找先这段话并注释掉 `<LocationMatch "^/+$">` `    Options -Indexes` `    ErrorDocument 403 /.noindex.html` `</LocationMatch>` 第七步、新建文件\[你网站域名\].conf，不要加点纯字母放在/opt/rh/httpd24/root/etc/httpd/conf.d目录 `<VirtualHost *:80>` `    DocumentRoot /home/www` `    ServerName xxx.com`    ###绑定域名 `</VirtualHost>` `<Directory "/home/www">` `    AllowOverride None` `    Options Indexes FollowSymLinks` `    # Allow open access:` `    Require all granted` `</Directory>` `service httpd24-httpd restart`   ##重启httpd进程设置完成 检查服务的命令 `service --status-all` `service --status-all grep ntpd` `service --status-all less` `service httpd status`