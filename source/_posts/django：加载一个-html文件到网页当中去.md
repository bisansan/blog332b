---
title: Django：加载一个.html文件到网页当中去
tags: []
id: '168'
categories:
  - - Django
date: 2018-10-22 15:01:35
---

现在项目templates新建一个index.html文件，在项目中做好url映射，在views.py设置如下函数 这个是代码示例一

from django.template.loader import render\_to\_string
from django.http import HttpResponse
def index(request):
    html = render\_to\_string("index.html")
    return HttpResponse(html)

这个是代码示例二

from django.shortcuts import render
def index(request):
    return render(request,"index.html")