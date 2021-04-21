---
title: 'Django :URL视图参数'
tags: []
id: '608'
categories:
  - - Django
date: 2019-03-28 17:17:50
---

1.创建一个普通的url映射

from django.urls import path
urlpatterns = \[
    path("",index),
\]

  2.主项目的urls.py总文件指向，可以在setting.py出更改ROOT\_URLCONF

ROOT\_URLCONF = 'xfz.urls'

  3.多个项目指定子urls.py方法 主urls.py文件，include后面为指定目录

from django.urls import path,include

urlpatterns = \[
    path('cms/',include('apps.cms.urls'))   
\]

  4.app命令空间防止在视图函数指定reverse("urlName")出现混乱，故可以这样设置reverse("AppZone:urlName") URL

app\_name = "appName"

urlpatterns = \[ 
    path("",views.index,name='index'), 
\]

视图

from django.shortcuts import redirect,reverse

def index(request):
        login\_url = reverse("appName:index")   //如果存在多个app,只有index是无法让django识别的
        return redirect(login\_url)