---
title: Django模板：自定义一个过滤器
tags: [django,python]
id: '208'
categories:
  - - 计算机编程
abbrlink: 697646bf
date: 2018-10-26 11:06:21
---

过滤器必须在任意app目录下载新建一个templatetags文件名的包，里面必须有\_\_init\_\_.py文件，将一个函数封装为过滤器时，一个函数最多只能有两个参数，新建一个article的app，在templatetags文件夹新建一个my\_filter.py文件

from django import template     ###导入模板函数

register = template.Library()

####@register.filter       这一行和最后一行语法一样，取其一即可
def greet(value,word):
    return value + word

register.filter("greet",greet)    ###我是最后一行

在项目setting.py文件的`INSTALLED_APPS` 导入article这个app，在模板中调用这个过滤器方法

{ % load my\_filter %}         #####在模板中导入过滤器
{ { "张三"greet:"你好" } }      ####输出结果为张三你好