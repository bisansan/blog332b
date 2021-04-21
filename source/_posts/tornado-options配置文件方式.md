---
title: tornado.options配置文件方式
tags: []
id: '850'
categories:
  - - uncategorized
abbrlink: 67c2328e
date: 2019-09-25 10:58:26
---

控制台日志可以通过下面命令关闭

```
from tornado.options import options, parse_command_line
options.logging = None
parse_command_line()
```

在元素内的配置方法

ornado.options.define用来定义数据，tornado.options.options用来访问数据

```
# 设置和声明对应的值
tornado.options.define("mysql_host", default="127.0.0.1:3306", help="Main user DB")

# 访问该值
print(tornado.options.options.mysql_host)
```

1.命令行来配置 tornado.options.parse\_command\_line

注意：这个方式不支持字典

```
# 执行python -m server.py --good=good
# 先声明
tornado.options.define("good", default="", help="Main user DB")
# 在获取
tornado.options.parse_command_line()
# 访问该值
print(tornado.options.options.good)
```

2.设置配置文件tornado.options.parse\_config\_file

注意：这个方式不支持字典

先创建config.conf文件

```
# config.conf
good = 'good'

port = 80
mysql_host = 'mydb.example.com:3306'
# Both lists and comma-separated strings are allowed for
# multiple=True.
memcache_hosts = ['cache1.example.com:11011',
                  'cache2.example.com:11011']
memcache_hosts = 'cache1.example.com:11011,cache2.example.com:11011'
```

再使用

```
# 先声明
tornado.options.define("good", default="", help="Main user DB")
# 设置文件路径
tornado.options.parse_config_file('config.conf')
# 访问该值
print(tornado.options.options.good)
```

3.直接使用py来创建，再用模块导入，不使用 tornado.options

```
# a.py
good = 'good'

# b.py
import a
print(a.good) 
```