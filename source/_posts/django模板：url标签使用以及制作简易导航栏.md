---
title: Django模板：URL标签使用以及制作简易导航栏
tags: []
id: '193'
categories:
  - - Django
date: 2018-10-24 14:11:21
---

在标签中我们经常要写一些url，在模板中使用反转，可以灵活的改动，方便易维护 一个普通的url反转参数示例

path("book/", book,name="book"),   ###url.py

<a href="{ % url "book" %}">读书</a>   ###index.html

一个带有关键词参数的反转示例

path("book/<fenlei>/detail/<book\_id>",book\_detail,name="book\_detail") #url.py

<a href="{ % url "book\_detail" fenlei="111" book\_id="1"  %}">最火的一篇文章</a>  ###index.html

一个带有查询字符串的反转

def login(request):
    next = request.GET.get("next")
    btext = "登录后跳转的url是：%s" % next
    return HttpResponse(btext)
path("login/",login,name="login"),   ####urls.py

<a href="{ % url "login" %}?next=aaaaa">登录</a>   ####index.html

url.py文件

from django.contrib import admin
from django.urls import path
from django.shortcuts import render
from django.http import HttpResponse
def index(request):
    text = {

    }
    return render(request,"index.html",context=text)
def login(request):
    next = request.GET.get("next")
    btext = "登录后跳转的url是：%s" % next
    return HttpResponse(btext)
def book(request):
    return HttpResponse("读书首页")
def movie(request):
    return HttpResponse("电影首页")
def kanbao(request):
    return HttpResponse("看报首页")
def book\_detail(request,book\_id,fenlei):
    atext = "你的书籍ID是：%s,分类是：%s" % (book\_id,fenlei)
    return HttpResponse(atext)
urlpatterns = \[
    path('admin/', admin.site.urls),
    path("",index,name="index"),
    path("book/", book,name="book"),
    path("movie/", movie,name="movie"),
    path("kanbao/", kanbao,name="kanbao"),
    path("book/<fenlei>/detail/<book\_id>",book\_detail,name="book\_detail"),
    path("login/",login,name="login"),
\]

index.html文件

<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .nav{
            overflow:hidden;
        }
        .nav li{
            float:left;
            list-style: none;
            margin: 0 20px;
        }
    </style>
</head>
<body>
    <ul class="nav">
        <li><a href="/">首页</a></li>
        <li><a href="{ % url "movie" %}">电影</a></li>
        <li><a href="{ % url "book" %}">读书</a></li>
        <li><a href="{ % url "kanbao" %}">看报</a></li>
        <li><a href="{ % url "book\_detail" fenlei="111" book\_id="1"  %}">最火的一篇文章</a></li>
        <li><a href="{ % url "login" %}?next=aaaaa">登录</a></li>
    </ul>
</body>
</html

截图 ![](https://post.332b.com/wp-content/uploads/2018/10/20181024141000-300x39.png)