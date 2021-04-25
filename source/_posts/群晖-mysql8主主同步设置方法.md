---
title: 群晖 mysql8主主同步设置方法
tags: [synology,mysql]
id: '1049'
categories:
  - - 技术教程
abbrlink: ddfd5a8e
date: 2021-01-08 10:03:11
---

## 群晖 mysql8主主同步设置方法

1.设置docker路径映射

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217174504.png)

2.设置环境变量

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217174648.png)

配置文件1

```
[mysqld]
.
```

3.进入容器执行命令

显示所有在用的容器

```
docker ps
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217175009.png)

进入容器执行命令

```
docker exec -it ccaf2b85392e bash
```

进入mysql执行命令

```
mysql -u root -p
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217175230.png)

创建同步使用的用户名和账户

```
CREATE USER 'sync'@'%' IDENTIFIED WITH mysql_native_password BY 'sync6123510';
```

赋予账号同步权限

```
 GRANT REPLICATION SLAVE,REPLICATION CLIENT ON *.* TO 'sync'@'%';
```

刷新数据库权限

```
flush privileges;
```

显示server\_id同步id，每个数据库id必须不一样

```
show variables like 'server_id';
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217175616.png)

查看mysql的master状态，注意图中的File和Position所对应的值

```
SHOW MASTER STATUS;
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217175834.png)

在另一台服务器上进入mysql执行界面后，添加上面这个数据的连接方式

```
mysql> CHANGE MASTER TO
    -> MASTER_HOST='114.114.114.114',
    -> MASTER_USER='sync',
    -> MASTER_PASSWORD='sync123',
    -> MASTER_LOG_FILE='mysql-bin.000003',
    -> master_port=6306,
    -> MASTER_LOG_POS=848;
Query OK, 0 rows affected, 2 warnings (0.93 sec)
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/QQ0201217180311.png)

启动同步

```
start slave;
```

查看同步状态

```
show slave status\G
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217180859.png)

连接失败重置一下slave

```
stop slave;

reset slave;

start slave;
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img/20201217182049.png)

给同步账号提升账号权限

```
GRANT ALL PRIVILEGES ON *.* TO 'sync'@'%';
flush privileges;
stop slave;
start slave;
```

检查master设置，如果错误就修改

```
CHANGE MASTER TO MASTER_LOG_FILE='mysql-bin.000002',MASTER_LOG_POS=155;
```