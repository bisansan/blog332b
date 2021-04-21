---
title: 简单的玩一下MYSQL 8.0
tags: []
id: '868'
categories:
  - - uncategorized
abbrlink: '47070840'
date: 2019-09-30 15:33:12
---

创建一个数据库，并设置编码为utf-8 mb4

```
CREATE SCHEMA `demo_1` DEFAULT CHARACTER SET utf8mb4 ;
```

在这个数据库底下创建一个new\_table表，并设置三个字段分别为id、name、age和bron\_date，id设为主键

```
CREATE TABLE `demo_1`.`new_table` (
  `id` INT NOT NULL,
  `name` VARCHAR(255) NULL,
  `age` INT NULL,
  `bron_data` DATE NULL,
  PRIMARY KEY (`id`));
```

接下来是新增两条数据试试

```
INSERT INTO `demo_1`.`new_table` (`id`, `name`, `age`, `bron_data`) VALUES ('1', 'fan', '18', '1994-05-06');
INSERT INTO `demo_1`.`new_table` (`id`, `name`, `age`, `bron_data`) VALUES ('2', 'key', '34', '1996-05-07');
```

新增了这些数据之后，不满意想修改

```
UPDATE `demo_1`.`new_table` SET `age` = '22', `bron_data` = '1992-05-07' WHERE (`id` = '2');
UPDATE `demo_1`.`new_table` SET `age` = '20', `bron_data` = '1998-08-12' WHERE (`id` = '1');
```

现在我不想要这些数据了，我要把他们删除了

```
DELETE FROM `demo_1`.`new_table` WHERE (`id` = '2');
DELETE FROM `demo_1`.`new_table` WHERE (`id` = '1');
```