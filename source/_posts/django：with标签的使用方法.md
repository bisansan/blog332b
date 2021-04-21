---
title: Django：with标签的使用方法
tags: []
id: '186'
categories:
  - - Django
date: 2018-10-23 17:38:26
---

在使用with标签的时候，我们输入`zs=person.0` 这个相等关系之间是不能有任何空格，with标签的主要作业是定义是在模板中定义变量，一直是with xx=xxx，另外一种是with xx as xxxx，变量只能爱当前with标签生效，开始于with结束于endwith urls.py文件

from django.contrib import admin
from django.urls import path
from django.shortcuts import render
def index(request):
    text = {
        "person":\[
            "张三",
            "李四",
            "王二",
            "铁蛋"
        \]
    }
    return render(request,"index.html",context=text)

urlpatterns = \[
    path('admin/', admin.site.urls),
    path("",index)
\]

index.html文件

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
{ % with zs=person.0 %}
    <p>{ { zs } }</p>
    <p>{ { zs } }</p>
    <p>{ { zs } }</p>
{ % endwith %}
{ % with person.1 as zs %}
        <p>{ { zs } }</p>
{ % endwith %}
</body>
</html>

截图 ![](https://post.332b.com/wp-content/uploads/2018/10/20181023173805.png)