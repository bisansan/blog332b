---
title: Django制作一个简易图书管理系统
tags: []
id: '240'
categories:
  - - Django
date: 2018-11-09 16:52:05
---

这个代码只适合学习，链接：[https://pan.baidu.com/s/1nVP9ikQPPnZP8cetoGNYcA](https://pan.baidu.com/s/1nVP9ikQPPnZP8cetoGNYcA) 提取码：0ldy 我们来试试先将setting.py中的django.middleware.csrf.CsrfViewMiddleware注释掉，关闭默认的csrf保护

\#    'django.middleware.csrf.CsrfViewMiddleware',

Django视图函数中实现POST和GET的请求，GET一般作为作为网址参数，它是明文的，POST跟服务器之间是密文发送

def func(request):
    post = request.POST.get  ####我是POST
    get = request.GET.get    ####我是GET
    if request.method == 'get':  ####可以获取访问清单的状态
        pass

效果图片展示 ![](https://post.332b.com/wp-content/uploads/2018/11/20181109164710.png)