---
title: python ORM数据库操作框架大全
tags: [mysql,orm]
id: '882'
categories:
  - - 计算机编程
abbrlink: c2ed5e85
date: 2019-10-28 13:49:03
---

![](https://post.332b.com/wp-content/uploads/2019/10/ORM_Perf-1024x451.png)

python ORM框架对比图，来自 Tortoise ORM 官网，仅供参考

1.django 内置OREM框架

django自带框架，不能与其他程序配合，django独有的

2\. peewee

链接： [https://pypi.org/project/peewee/](https://pypi.org/project/peewee/)

文档： [http://docs.peewee-orm.com/en/latest/](http://docs.peewee-orm.com/en/latest/)

安装方式

```
pip install peewee
```

3.storm

链接： [https://pypi.org/project/storm/](https://pypi.org/project/storm/)

安装方式：

```
pip install storm
```

4.SQLAlchemy

链接： [https://pypi.org/project/SQLAlchemy/](https://pypi.org/project/SQLAlchemy/)

文档： [https://docs.sqlalchemy.org/en/13/](https://docs.sqlalchemy.org/en/13/)

安装方式

```
pip install SQLAlchemy
```

5.sqlobject

链接： [https://pypi.org/project/SQLObject/](https://pypi.org/project/SQLObject/)

文档： [http://www.sqlobject.org/#documentation](http://www.sqlobject.org/#documentation)

安装方式

```
pip install SQLObject
```

6.pony

链接：[https://pypi.org/project/pony/](https://pypi.org/project/pony/)

文档： [https://docs.ponyorm.org/](https://docs.ponyorm.org/)

安装方式

```
pip install pony
```

7.Tortoise

使用了新特性 asyncio 的构造的orm框架，需要较新的python 3.6+,，只支持SQLite和MySQL，将来有可能会有变动，建议先观察

链接： [https://pypi.org/project/tortoise-orm/](https://pypi.org/project/tortoise-orm/)

文档：[https://tortoise-orm.readthedocs.io/en/latest/](https://tortoise-orm.readthedocs.io/en/latest/)

```
pip install tortoise-orm
```