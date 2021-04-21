---
title: 'Python3:返回一个中文时间值'
tags: []
id: '134'
categories:
  - - Python
abbrlink: 6a98a665
date: 2018-10-11 10:29:34
---

使用time.strftime直接添加中文会报错，会显示下面的错误

UnicodeEncodeError: 'locale' codec can't encode character '\\u7684' in position 4: Illegal byte sequence

可以直接修改成下面代码，返回中文格式化时间

time.strftime('%Y{y}%m{m}%d{d} %H{h}%M{f}%S{s}').format(y='年',m='月',d='日',h='时',f='分',s='秒')

time模块的其他用法

import time
print("time.time时间戳:",time.time())
print("time.localtime本地时间struct\_time:",time.localtime())
print("time.gmtime标准UTC +0时间:",time.gmtime())
print("将struct\_time转换成时间戳：",time.mktime(time.localtime()))
print(time.strftime("%Mds的"),time.localtime())

将某些中文显示时间转换成struct\_time的方法

a,b = '2017年7月23日9时1分1秒',"年月日时分秒"
for i in b:a = a.replace(i," ",1)
print(time.strptime(a,"%Y %m %d %H %M %S "))