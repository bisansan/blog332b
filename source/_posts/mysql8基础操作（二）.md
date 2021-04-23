---
title: mysql8基础操作（二）
tags: [mysql]
id: '1055'
categories:
  - - 系统运维
abbrlink: de755416
date: 2020-12-06 21:23:04
---

mysql8基础操作

1.union（去重，需要更多的性能）和union all（不会去重，速度快）查询结果对比

```
SELECT * FROM A UNION SELECT * FROM B
SELECT * FROM A UNION ALL SELECT * FROM B
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201218160149.png)

2.笛卡尔集现象

```
SELECT * FROM A,B
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201218162628.png)

3.去除笛卡尔集，添加条件筛选

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201222101509.png)

4.内连接查询，inner join 就等于 join

![](https://gitee.com/wittzhang/pic332b/raw/master/img//img_innerjoin.gif)

```
SELECT * FROM A name_a INNER JOIN B name_b on name_a.`name` = name_b.`name` WHERE name_b.score > 30;
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201222104349.png)

5.左外连接查询，取左边的表的全部，右边的表按条件，符合的显示，不符合则显示null，left outer join 与 left join 等价， 一般写成left join

![](https://gitee.com/wittzhang/pic332b/raw/master/img//1074709-20171229170434726-2010021622.png)

```
SELECT * FROM A name_a LEFT JOIN B name_b on name_a.`name` = name_b.`name`;
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201222105222.png)

6.右外连接查询，取右边的表的全部，左边的表按条件，符合的显示，不符合则显示null，right outer join 与 right join等价，一般写成right join

![](https://gitee.com/wittzhang/pic332b/raw/master/img//1074709-20171229171503867-2027149651.png)

```
SELECT * FROM A name_a RIGHT JOIN B name_b on name_a.`name` = name_b.`name`;
```

![](https://gitee.com/wittzhang/pic332b/raw/master/img//20201222105728.png)

7.多表联合查询

```
SELECT * FROM A name_a JOIN B name_b RIGHT JOIN C name_c on name_a.`name` = name_b.`name` AND  name_b.`name` = name_c.`name`;
```

![image-20201222111033326](https://gitee.com/wittzhang/pic332b/raw/master/img//image-20201222111033326.png)