---
title: Django：向网页输出以字典key和列表中值
tags: []
id: '170'
categories:
  - - Django
abbrlink: b45c3548
date: 2018-10-22 17:39:54
---

请先映射好URL链接，注意字典中的keys不能跟dict的语法同名，否者会造成冲突，views.py代码

from django.shortcuts import render
def index(requuest):
    xcontext = {
        "username" :"admin"
    }
    return render(requuest,"index.html",context=xcontext)

模板index.html源码

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{ { username } }
</body>
</html>

这个是一个类，面对对象的引用方法 views.py文件代码

from django.shortcuts import render
class Person(object):
    def \_\_init\_\_(self,username):
        self.username = username
def index(requuest):
    p = Person("zhiliao")
    context = {
        "person" :p
    }
    return render(requuest,"index.html",context=context)

模板文件index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{ { person.username } }
</body>
</html>

# 这个是获取列表中的值的方法

例如python中有个列表`p = ["你好","很好","非常好"]` ，在模板中怎么去实现呢？ 在模板不能用中括号，写入的方式类似字典，例如我要输出p列表中的第一个值，就这样写`{ { p.0 } }`