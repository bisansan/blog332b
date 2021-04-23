---
title: Django实现首页不带参数访问目录第一页
tags: [django,python]
id: '166'
categories:
  - - 计算机编程
abbrlink: 7882ff88
date: 2018-10-22 14:35:46
---

这段代码实现首页访问到目录页第一页，不用在后面加代码

from django.urls import path
from django.http import HttpResponse
atext = \["红楼梦","水浒传","安徒生通话"\]
def index(requset,book\_id=0):
    return HttpResponse(atext\[book\_id\])
urlpatterns = \[
    path("",index),
    path("page/<int:book\_id>",index)
\]