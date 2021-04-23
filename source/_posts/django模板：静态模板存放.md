---
title: Django模板：静态模板存放规则和目录
tags: [django,python]
id: '226'
categories:
  - - 计算机编程
abbrlink: 51508a34
date: 2018-11-02 16:07:33
---

1、查看项目setting.py文件INSTALLED\_APPS里面有没有`'django.contrib.staticfiles'` 2、查看项目setting.py文件STATIC\_URL设置没有`STATIC_URL = '/static/'` 3、存放静态文件的方法，先创建一个app，并且在setting.py里面INSTALLED\_APPS添加app，在app目录创建static目录，以后静态文件都可以放在static目录，用户在访问的时候，Django就会在static目录查找文件

{ % load static %}     ###载入静态文件目录
{ % static "2018.png" %}     ##载入2018.png文件

4.如果存在多个app，Django会在多个static目录查找文件，这样就会造成混淆，为了避免这种情况python建议的是你在当前app/static目录存放文件，那就在当前app/static再创建跟当前app一样的名字文件夹，例如：app/static/app，对应的url是www.xxx.com/static/app/,用户和Django访问和查找文件的时候就不会混淆了 5.设置一个独立的static目录方法，在setting.py最后一行添加如下文本，这个是跟主项目templates一样放在同级别目录

STATICFILES\_DIRS = (
    os.path.join(BASE\_DIR,'static'),
)

6.每个html模板都要向下面这样load一下，我们才能载入静态标签非常麻烦

{ % load static %}      ###载入静态文件目录

在setting.py添加如下内容，就可以不要在每个模板中load，直接把static变成一个内置标签，在TEMPLATES中的OPTIONS添加`'builtins':['django.templatetags.static'],`

TEMPLATES = \[
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': \[os.path.join(BASE\_DIR, 'templates')\]
        ,
        'APP\_DIRS': True,
        'OPTIONS': {
            'builtins':\['django.templatetags.static'\],
            'context\_processors': \[
                'django.template.context\_processors.debug',
                'django.template.context\_processors.request',
                'django.contrib.auth.context\_processors.auth',
                'django.contrib.messages.context\_processors.messages',
            \],
        },
    },
\]

7.当setting.py没有`'django.contrib.staticfiles'` 的另外一种替换方法，不过它对比之前的只能在主项目的static放静态文件，在app/static目录存放文件无效，这个方法是修改urls.py文件

from django.conf.urls.static import static
from django.conf import settings
urlpatterns = \[
    
\] + static(settings.STATIC\_URL,document\_root=settings.STATICFILES\_DIRS\[0\])
####这个模板返回的是一个列表，所以要使用到加号