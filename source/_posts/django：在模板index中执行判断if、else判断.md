---
title: Django：在模板index中执行判断if、else判断
tags: []
id: '180'
categories:
  - - Django
date: 2018-10-23 15:32:03
---

在Django模板中执行判断语句，可以执行if判断语句，它必须以{ % if %}开始，以{ % endif %if}结束，在模板中快速生成一个if和endif的快捷键为输入if后按下Tab键，在模板中使用注释的快捷键是Ctrl + / if判断url.py文件示例

from django.urls import path
from django.shortcuts import render

def index(request):
    return render(request,"index.html",context=text)
text ={
    "age":18
}

urlpatterns = \[
    path('admin/', admin.site.urls),
    path("",index)
\]

index.html示例

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
首页
{ % if age < 18 %}
    <p>你是未成年人，不能进入网吧</p>
{ % elif age >= 18 %}
    <p>你已经成年，可以进入网吧了</p>
{ % else %}
    <p>貌似有点异常</p>
{ % endif %}
</body>
</html>