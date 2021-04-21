---
title: 腾讯云Ubuntu 18.04 监控工具zabbix安装方法
tags: []
id: '658'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
date: 2019-06-04 17:04:53
---

使用Ubuntu能最大的节省我们的时间，将最大的时间放在业务上，研究那些开源安装方法实在太折腾人了，这里使用的是官方推荐的源，然后结合宝塔面板一起使用，方便软件管理和后期升级！   1、先将服务器软件更新到最新 sudo apt update sudo apt upgrade   2.安装zabbix后端服务器 wget https://repo.zabbix.com/zabbix/4.2/ubuntu/pool/main/z/zabbix-release/zabbix-release\_4.2-1+bionic\_all.deb sudo dpkg -i zabbix-release\_4.2-1+bionic\_all.deb sudo apt update #这里放弃安装zabbix-frontend-php，使用宝塔面板来管理前端界面，简化我们的管理操作 sudo apt -y install zabbix-server-mysql zabbix-agent   3.安装宝塔面板 wget -O install.sh http://download.bt.cn/install/install-ubuntu\_6.0.sh && sudo bash install.sh # 安装完后，一定要保存好控制台上的信息，可以保存在电脑文件里 ![](https://post.332b.com/wp-content/uploads/2019/06/20190604161102.png) #请自己登陆后台，安装好apache和php，不要安装mysql，因为已经zabbix自己已经安装了，再安装会冲突   4.导入数据库文件 重置mysql数据库root密码参考：[https://www.cnblogs.com/roadofstudy/p/7446690.html](https://www.cnblogs.com/roadofstudy/p/7446690.html) # mysql -uroot -p mysql> create database zabbix character set utf8 collate utf8\_bin; mysql> grant all privileges on zabbix.\* to zabbix@localhost identified by '设置zabbix数据密码'; mysql> quit;   数据库文件获取参考第6步，在解压后的database\\mysql目录 数据导入命令：mysql -u root -p zabbix < schema.sql 可以这样导入数据库 依次导入 schema.sql 》 images.sql 》data.sql   编辑 /etc/zabbix/zabbix\_server.conf，找到下面这行取消注释填入你的密码 `DBPassword=password`   5.启动zabbix后端 systemctl restart zabbix-server zabbix-agent      #重新启动 systemctl enable zabbix-server zabbix-agent     #开机自启 systemctl status zabbix-server.service      #查看服务启动状态 如果启动失败，可以查看/var/log/zabbix/zabbix\_server.log，根据log来处理相应的错误   6.安装前台 下载开源zabbix：https://www.zabbix.com/download\_sources 解压后找到frontends/php上传到网站根目录， 数据库选项和上面填填一样，数据库名和用户名也是zabbix 后台默认登陆密码是Admin，密码zabbix   小问题总结 ？zabbix后台管理不能选中文 需要安装中文环境，最少要选择zh\_CN utf-8 utf-8 sudo dpkg-reconfigure locales