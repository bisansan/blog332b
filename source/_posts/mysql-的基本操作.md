---
title: Mysql 的基本操作
tags: [mysql]
id: '460'
categories:
  - - 系统运维
abbrlink: 1b033b27
date: 2019-01-16 17:29:08
---

**一、修改/etc/mysql/my.conf** 找到bind-address = 127.0.0.1这一行 改为bind-address = 0.0.0.0即可 **二、为需要远程登录的用户赋予权限** 1、新建用户远程连接mysql数据库 grant all on \*.\* to admin@'%' identified by '123456' with grant option; flush privileges; 允许任何ip地址(%表示允许任何ip地址)的电脑用admin帐户和密码(123456)来访问这个mysql server。 注意admin账户不一定要存在。 2、支持root用户允许远程连接mysql数据库 grant all privileges on \*.\* to 'root'@'%' identified by '123456' with grant option; flush privileges; 修改数据库密码     mysqladmin -u root -p password 123456 mysql 5.6之前版本： update user set password=password('abc') where User='root'; mysql 5.7版本： update mysql.user set authentication\_string=password('123456') where user='root' and host='%';; mysql 8.0版本：ALTER user 'root'@'localhost' IDENTIFIED BY '123456' 显示所有数据库 show databases 创建数据库 创建一个my\_test数据库，并将它的数据库编码设置为utf8编码 create database my\_test character set utf8; ##character \[ˈkærəktɚ\]  特征，特点； 选择和进入一个数据库   use my\_test; 删除指定数据库   drop database user; 数据库一旦创建，名称是无法修改的，在mysql数据库中，字符串类型和日期类型的数据，必须要使用单双引号

## 数据定义语言DDL

**查询** 显示所有表 show tables 查看表字段   desc user ##desc在SQL语言中，代表降序 查看表详细结构，包含创建命令，表编码，表类型 show create table uers; **新增** 新建表 新建一个名称叫user的表，它包含三个字段id设置为整数，username设置为最长10位字符串，password最长为16位 create table user(id int,username varchar(10),password varchar(16)); 新增表字段 在一个表中新增一个mail字段，最大长度为30位 alter table user add mail varchar(30); ##alter \['ɔltɚ\]    变更，改变； **修改** 修改表字段数据类型 修改user表id字段的类型为bigint alter table user modify id bigint; #modify  \[ˈmɑdɪfaɪ\]    修改，修饰； 修改表的称 将表user改名为users rename table user to users; 修补表编码 修改users表的编码为utf8 alter table users character set utf8; 修改表的字段名（列名） 修改user表下的mail字段，新命名为mails数据类型varchar，限制成30位 alter table users change mail mails varchar(30); **删除** 删除表 drop table users; 删除表字段 删除一列的邮箱字段 alter table user drop mail; ##drop \[drɑp\] 下降，终止；

## 数据操作语言DML

**查询** 查询表数据 查看users表所有数据 select \* from users 查询指定列(字段)所有数据 select username,mails from users **新增** 新增(插入)表数据 在users新增一个id为2，名称为admin，密码为123456，邮箱为123@qq.com的数据，命令全部用空格隔开 insert into users (id,username,password,mails) values (2,'admin','123456','123@qq.com'); 新增(插入)表多个数据 插入多个数据时，将多个数据用逗号‘ , ’隔开 insert into users (id,username,password,mails) values (1,'user','123456','user@qq.com'),(2,'admin','123456','123@qq.com'); **修改** 更改表数据 更新users表id为2的所有数据，将username更为‘admin’，如果没有where指定条件，则会更新这个表的全部数据的username update users set username='admin' where id=2; 表数据运算 更新users表username=‘admin’的所有数据，将id加1，除了加法，还可以加减乘除，但必须是数字；如果没有where指定条件，则会更新这个表的全部数据的id update users set id=id+1 where username='admin'; **删除** 删除表中的所有的所有数据 delete from users; 删除表中的指定数据 删除users表中的id为1的数据 delete from users where id=1 清空表结构，并重新创建同样的表覆盖原表 它跟delete的区别是，delete支持数据找回，truncate不支持数据找回，并且truncate比delete执行速度快 truncate table users;

## 数据查询语言DQL

**条件查询** where后面可以跟的查询条件

1.  \=（等于），!=（不等于，<>（不等于），<（大于），>（小于），<=（大于或等于），>=（小于或等于）；
2.  between ......and :值在什么范围
3.  in(1,2)    是否在这个范围里面
4.  is null（为空）和is not null（不为空）
5.  and: 与
6.  or：或者
7.  not；非

根据上面的查询条件，给一些示例

1.  查询id大于3  select \* from users where id>3;
2.  查询id的值在1和5之间的   select \* from users where id between 1 and 5;
3.  查询id的值等于1、2和3    select \* from users where id in(1,2,3);
4.  查询id不为空的   select \* from users where id is not null;
5.  查询id等于1和username等于a123的     select \* from users where id=1 and username='a123'
6.  查询id等于1或者username等于a123的   select \* from users where id=1 or usernmae='a123'
7.  查询所有id不是1的    select \* from users where not id=1;

**模糊查询** 模糊查询关键字like，%代表任意几个字符，\_代表任意一个字符 查询users表username中以a字符开头和a字符结尾的任意字符 SELECT \* FROM users WHERE username LIKE 'a%' 查询users表username中以a字符开头和a字符结尾的任意4位组成的字符 SELECT \* FROM users WHERE username LIKE 'a\_\_a' **去重查询** 查询users表中的username字段并且去除重复字段 SELECT DISTINCT username from users; distinct   \[dɪˈstɪŋkt\]   明显的，清楚的; **查询结果运算** 对查询字段直接进行相加，要输数据都是数字 提取users所有的字段，生成一个新字段，新字段的值为id+3 SELECT \*,id+3 as newid from users; 判断如果id大于3就返回1，如果不大于3或者null就返回0 SELECT \*,IF(id>3,1,0) as newid from users; IFNULL(expr1,expr2)   expr1为判断对象，如果为null，那么它的值就为expr2 **查询排序** 倒序排序从大到小，默认是ASC从小到大 查询users里面的表，按照id从大到小排序 SELECT \* from users ORDER BY id DESC; 指定二级排序 查询users里面的表，按照id从大到小排序，两个id一样时，那两个一样的id就按照number进行从大到小的排序 SELECT \* from users ORDER BY id DESC,number DESC; **聚合函数** count 统计 统计表数据总数 统计users表中总共有多少条数据 SELECT COUNT(\*) FROM users; 统计字段数据总数 统计在表中有id的数据总共有多少条，如果id为none就不会统计改值 SELECT COUNT(id) FROM users; 它后面还可以更上条件查询where，例如我们想查询id大于3数据的总数 SELECT COUNT(id) FROM users WHERE id>3; AVG 统计平均值，SUM统计总和 统计id值大于3的总和and平均数 SELECT AVG(id),SUM(id) FROM users WHERE id>3; MAX 最大数，MIN最小数 统计id值大于3的最大值and最小值 SELECT MAX(id),MIN(id) FROM users WHERE id>3; GROUP BY分组查询

1.  GROUP BY  分组统计id字段
2.  GROUP\_CONCAT(score)  统计按照id来进行分组，score字段的所有数据
3.  MIN(score)      统计每组score中最小值
4.  MAX(score)     统计每组score中最大值

SELECT id,GROUP\_CONCAT(score),MIN(score),MAX(score) FROM users GROUP BY id; ![](https://post.332b.com/wp-content/uploads/2019/01/QQ截图20190123172412.png) Hvaing二次条件查找 除了WHERE可以进行条件查找，HAVING可以根据WHERE查找出来的数据，进行二次查找 SELECT id FROM users WHERE id>2 HAVING s>50; WHERE和HAVING的区别 1.HAVING可以使用聚合函数，而WHERE不能使用聚合函数 2.HAVING可以放在GROUP BY后面，配合它进行结合使用，而WHERE必须放在GROUP BY的前面 SQL查询语句书写循序： select > from > where > GROUP BY > having > order by > limit 选择字段  》 来自哪个表 》查询条件 》分组查询 》二次条件查询 》排序