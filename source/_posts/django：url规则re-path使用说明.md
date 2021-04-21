---
title: Django：URL规则re_path使用说明
tags: []
id: '156'
categories:
  - - Django
date: 2018-10-19 16:31:16
---

应用文件夹urls.py：

from django.urls import re\_path
from . import views
urlpatterns = \[
    re\_path("^$",views.app\_one),
    re\_path(r"^list/(?P<youinput>\\d{3}).html",views.app\_three),
##对应的www.xxx.com/list/xxx.html
    re\_path(r"^book\_(?P<youinput>\\d{3})\_(?P<youe>\\d{3})",views.app\_two)
##对应的www.xxx.com/book\_xxx\_xxx
\]

应用文件夹views.py：

from django.http import HttpResponse
def app\_one(request):
    return HttpResponse("APP首页")
# Create your views here.
def app\_two(request,youinput,youe):
    texta = "你的输入的是：%s"% youinput,youe
    return HttpResponse(texta)

def app\_three(request,youinput):
    textb = "你的输入的是：%s"% youinput
    return HttpResponse(textb)

能用path就尽量用path，除非要使用正则表达式才用re\_path这样不会把简单的事情搞得复杂