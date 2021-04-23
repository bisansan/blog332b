---
title: Django：相关的时间处理pytz模块navie和aware时间
tags: [django,python]
id: '262'
categories:
  - - 计算机编程
abbrlink: 72f1cf69
date: 2018-11-12 14:06:33
---

# navie和aware时间的区别

navie时间是不知道自己表示的是那个时区的时间 aware时间是明确的知道自己是那个时区的时间 ##注意：在windows中，这个选项被系统优化了

# pytz库:

在安装django的时候就会自动安装pytz库，它可以协助我们Django来处理时间

# astimezone方法：

将一个时区的时间转换成另一个时区的时间，这个转换对象不能为navie时间

# replace

可以将时间的某些属性进行更改 import pytz from datetime import datetime now = datetime.now()   ##这是一个navie时间 utc\_timezone = pytz.timezone("UTC")    ##定义一个UTC时间 utc\_timezone = now.astimezone(utc\_timezone)    ###将当前时间转换为UTC时区的时间 ---`ValueError: astimezone() requires an aware datetime   ##执行会抛出一个异常，原因是navie时间不能调用astimezone方法` now = now.replace(tzinfo=pytz.timezone('Asia/Shanghai'))     ###通过添加时区参数，将navie转换awaretime，这样就不会报错 utc\_timezone = now.astimezone(utc\_timezone)

# DateTimeField中的auto\_now\_add和

# auto\_now区别

time = models.DateTimeField(auto\_now\_add=True) ###models.py文件

auto\_now返回当前的时间，每次执行save都会将当前时间放入数据库，auto\_now\_add将当前时间放入数据库，如果已经执行了一次，就不会再执行

# 关于setting.py中的USE\_TZ和TIME\_ZONE

TIME\_ZONE = 'Asia/Shanghai'
USE\_TZ = True

如果你将USE\_TZ设为False，那么获取的就是一个navie时间，TIME\_ZONE设置成本机的时区，方便国际化

# django.utils.timezone中now和localtime

同时他也有个now.astimezone的用法，类似datatime,astimezone

import django.utils.timezone from now,localtime
now()       ###返回的是一个UTC时间
localtime(now())     ###返回的是一个本地时间

#  Django模版中的时间高级用法

当你把now()输出到模版之后，Django输出网页会自动转换成用户当地时间

{ % load nowtime %}        ##也可以这样{ % load nowtimelocaltime %}