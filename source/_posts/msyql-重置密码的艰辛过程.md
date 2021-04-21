---
title: MSYQL 重置密码的艰辛过程
tags: []
id: '860'
categories:
  - - uncategorized
date: 2019-09-29 11:28:15
---

此片文章针对的8.0.17，如果你是差不多的版本，只建议参考，mysql 版本变更，导致一些语法也变更了，所以根据自己的实际情况来

我参考了下面链接，发现还是有部分问题

[https://blog.csdn.net/shenwuwangc/article/details/83959239](https://blog.csdn.net/shenwuwangc/article/details/83959239)

先停掉mysql，然后用下面的命令启动，就可以直接任意密码进入

```
mysqld --console --skip-grant-tables --shared-memory
```

先提供几个加密方式，以及对应的密码

```
# 加密方式      密码      加密后的字符串
# mysql_native_password     admin123    *01A6717B58FF5C7EAFFF6CB7C96F7428EA65FE4C
# 加密方式同上        S.admin123        *55778FA997BB023415F8507D1FAB1B380E83C011
```

查看root密码的加密方式，主机地址等等

```
mysql> select user,host,plugin,authentication_string from mysql.user where user='root';
+------+-----------+-----------------------+-----------------------+
 user  host       plugin                 authentication_string 
+------+-----------+-----------------------+-----------------------+
 root  localhost  mysql_native_password                        
+------+-----------+-----------------------+-----------------------+
1 row in set (0.00 sec)
```

开始设置自己的密码，密码你可以选择自己想要的，我选择的是admin123

```
mysql> update mysql.user set authentication_string='*01A6717B58FF5C7EAFFF6CB7C96F7428EA65FE4C' where user='root';
Query OK, 1 row affected (0.07 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

查看是否修改成功，非常棒，OK！，如果你的加密方式不是mysql\_native\_password，你可以将上面的语句改动一下即可

```
mysql>  select user,host,plugin,authentication_string from mysql.user where user='root';
+------+-----------+-----------------------+-------------------------------------------+
 user  host       plugin                 authentication_string                     
+------+-----------+-----------------------+-------------------------------------------+
 root  localhost  mysql_native_password  *01A6717B58FF5C7EAFFF6CB7C96F7428EA65FE4C 
+------+-----------+-----------------------+-------------------------------------------+
1 row in set (0.00 sec)
```

刷新一下执行权限，退出命令行，重启mysql登录

```
mysql> flush privileges;
Query OK, 0 rows affected (0.03 sec)

mysql> quit
Bye

G:\mysql\mysql-8.0.17-winx64\bin
λ net start mysql
MySQL 服务正在启动 ..
MySQL 服务已经启动成功。


# 注意下面的-P4000，是指定端口为4000，如果你端口是默认的3306，可以不用添加
G:\mysql\mysql-8.0.17-winx64\bin
λ mysql -u root -P4000 -p
Enter password: ********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.17 MySQL Community Server - GPL

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```