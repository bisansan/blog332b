---
title: mysql分组查询和聚合函数，数据截取和排序
tags: []
id: '888'
categories:
  - - '%e6%95%b0%e6%8d%ae%e5%ba%93'
    - Mysql
abbrlink: b232ec93
date: 2019-10-31 15:45:36
---

![](https://post.332b.com/wp-content/uploads/2019/10/20191031142611.png)

如图所示的上表，group by分组必须在select中存在，就在这样

```
正确
SELECT zuming AS new_id FROM demo GROUP BY zuming;
错误一，因为指定了zuming分组，而name却不知道怎么归类，所以报错了
SELECT name,zuming AS new_id FROM demo GROUP BY zuming
错误二
SELECT * FROM demo GROUP BY zuming 
```

上面的错误使用会引发sql\_mode=only\_full\_group\_by，这是因为sql语法越来越严谨了，具体关闭方法百度，不推荐关闭

在查询语句中使用了groups和group均报错，所以就换成 zuming

SELECT zuming AS new\_id FROM demo GROUP BY zuming;查询如图

![](https://post.332b.com/wp-content/uploads/2019/10/20191031143806.png)

如果我们要查询这个组的某个字段有那些值，我们可以用GROUP\_CONCAT

```
SELECT zuming,GROUP_CONCAT(name),GROUP_CONCAT(age) FROM demo GROUP BY zuming
```

![](https://post.332b.com/wp-content/uploads/2019/10/20191031144501.png)

如果GROUP BY指定了两个字段，就会这样，ORDER BY指定排序字段， DESC 可以让排序相反

```
SELECT name,age,zuming,GROUP_CONCAT(salary),COUNT(age) FROM demo GROUP BY zuming,name,age ORDER BY zuming DESC
```

![](https://post.332b.com/wp-content/uploads/2019/10/20191031151117.png)

GROUP BY 可以配合聚合函数来统计分组组的salary的总和，AS可以将字段改名

```
SELECT zuming,GROUP_CONCAT(name),GROUP_CONCAT(salary),SUM(salary) as salary_count FROM demo GROUP BY zuming
```

![](https://post.332b.com/wp-content/uploads/2019/10/20191031153129.png)

Limit number,number 第一个数字指定从第几个开始截取，第二个指定截取多少个

```
SELECT * FROM demo LIMIT 0,5
```

![](https://post.332b.com/wp-content/uploads/2019/10/20191031154311.png)