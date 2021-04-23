---
title: Django：上下文处理器和中间件
tags: [django,python]
id: '409'
categories:
  - - 计算机编程
abbrlink: 7eb155a5
date: 2018-12-19 17:46:51
---

## 上下文处理器

上下文处理器是可以返回一些数据，在全局摸板中都可以使用。比如登录后的用户信息，在很多页面中都需要使用，那么我们可以放 在上下文处理器中，就没有必要在每个视图函数中都返回这个对象。 在settings.TEMPLATES.OPTIONS.context\_processors中，有许多内晋的上下文处理器。这些上下文处理器的作用如下： 1. django.template.context\_processors.debug :増加一个debug和sql\_queries变量。在摸板中可以通过他来查看到一些数据库查询。 2. django.template.context\_processors.request :增加一个request变量。这个request变量也就是在视圈函数的第一个参数。 例如在模板中使用{ { request.path } }，就可以在模板中显示当前网址路径 3. django.contrib.auth.context\_processors.auth : Django有内置的用户系统，这个上下文处理器会増加一个user对象。 例如下面示例中context\['front\_user'\]，如果直接用\['user'\]可能会跟上面这个user冲突 4. django.contrib.messages.context\_processors.messages :増加一个 messages 变量 在模板中singin.py

<td>
    { % for message in messages %}
    { { message } }
    { % endfor %}
</td>

在视图views.py

from django.contrib import messages
messages.add\_message(request,messages.INFO,'用户名或者密码错误！')
#也可以这样写messages.info(request,'用户名和密码错误！')

5\. django.template.context\_processors.media :在模板中可以读取MEDIA\_URL比如想要在模板中使用上传的文件，那么这时候 就需要使用settings.py中设罝的MEDIA\_URL来拼接url示例代碍如下： `<img src="{ { MEDIA_URL} } { {user.avatar } }" /> `   user.avatar为存储到数据库的文件路径 6. django.template.conxext\_processors.static :在模板中可以使用 STATIC\_URL。 7. django.template.context\_processors.csrf :在模板中可以使用 csrf\_token 变量来生成一个 csrf\_token 在setting.py中context\_processors添加后，的直接在模板中的表单中添加

<input type="hidden" name="csrfmiddlewaretoken" value="{ { csrf\_token } }">

或者不添加，直接在模板中使用

{ % csrf\_token %}

自定义上下文处理器： 有时候我们想要返回自己的数据。那么这时候我们可以自定义上下文处理器。自定义上下文处理器的步骤如下： 1. 你可以根据这个上下文处理器是属于哪个app，然后在这个app中创建一个文件专门用来存储上下文处理器。比如context\_processors.py或者是你也可以专门创建一个Python,用来存储所有的上下文处理器。 setting.py

TEMPLATES = \[
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': \[os.path.join(BASE\_DIR, 'templates')\]
        ,
        'APP\_DIRS': True,
        'OPTIONS': {
            'context\_processors': \[
                'django.template.context\_processors.debug',
                'django.template.context\_processors.request',
                'django.contrib.auth.context\_processors.auth',
                'django.contrib.messages.context\_processors.messages',
                'front.context\_processors.front\_user',
            \],
        },
    },
\]

2\. 在你定义的上下文处理器文件中，定义一个函数，这个函数只有一个request参数。这个函数中处理完自己的逻辑后，把需要返 回给模板的数据，通过字典的形式返回。如果不需要返回任何数据，那么也必須返回一个空的字典。示例代码如下： context\_processors.py

from .models import User
def front\_user(request):
    user\_id = request.session.get('user\_id')
    context = {}
    if user\_id:
        try:
            user = User.objects.get(pk=user\_id)     ###因为get获取不到值，就会出现异常报错，所以要用try处理一下
            context\['front\_user'\] = user
        except:
            pass
    return context

## 中间件

中间件是在request和response处理过程中的一个插件。比如在request到达视圏数之前，我们可以使用中间件来做一些相关的 事情，比如可以判断当前这个用户有没有登录，如果登录了，就绑定一个user对象到request上。也可以response到达浏览器 之前，做一些相关的处理，比如想要统一在response上设罝一cookie信息等。 自定义中间件： 中间件所处的位置没有规定，只要是放到项目当中即可。一般分为两种情况，如果中间件是属于某个app的，那么可以在这 个app下面创建一个python文件用来存放这个中间件，也可以专门创建一个Python包，用来存放本项目的所有中间件。创建中间 件有两种方式，一种是使用函数、一种是使用类，接下来对这两种方式做个介绍： 在setting.py中添加

MIDDLEWARE = \[
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
    'front.middleware.Frontusermiddleware'
\]

类中间件的添加方法

class Frontusermiddleware(object):
    def \_\_init\_\_(self,get\_response):
        print('启动后执行的命令')
        self.get\_response = get\_response
    def \_\_call\_\_(self, request):
        print('request到达视图前执行的命令')
        user\_id = request.session.get('user\_id')
        if user\_id:
            try:
                user = User.objects.get(pk=user\_id)
                request.front\_user = user
            except:
                request.front\_user = None
        else:
            request.front\_user = None
        response = self.get\_response(request)    #####分割线
        print('response到达浏览器前执行的代码')    
        return response

函数添加中间键的方法

def front\_user\_middlewrae(get\_response):
    print('启动后执行的命令')
    def middleware(request):
        print('request到达视图前执行的命令')
        user\_id = request.session.get('user\_id')
        if user\_id:
            try:
                user = User.objects.get(pk=user\_id)
                request.front\_user = user
            except:
                request.front\_user = None
        else:
            request.front\_user = None
        response = get\_response(request)
        print('response到达浏览器前执行的代码')
        return response
    return middleware

1\. django.middleware.common.CommonMiddleware :通用中间件他的作用如下： 限制settings.DISALLOWED\_USER\_AGENTS中指定的请求头来访问本网站。DISALLOWED\_USER\_AGENTS是一个正则表达式的列表。示例代码如下：

import re

DISALLOWED\_USER\_AGENTS =\[

    re.compile(r'^\\s$^$'),

    re .compile(r'.\*PhantomJS.\*')

\]

2.django.middleware.gzip.GZipMiddleware :将响应数据进行压缔。如果内容长度少于200个长度，那么就不会压缩。 3.django.contrib.messages.middleware.MessageMiddleware :消息处理相关的中间件。 4. django.middleware.security.SecurityNiddleware :做了一些安全处理的中件。比如设置XSS防御的请求头，比如做了http协议转https协议的工作等。 5. django.contrib.sessions.middleware.SessionMiddleware : session中间件。会给request 添加—个处理好的session对象。 6.django.contrib.auth.middleware.AuthenticationMiddleware :会给request添加一个user对象的中间件。 7. django.middleware.csrf.CsrfViewMiddleware : CSRF 保护的中间件。 8. django.middleware.clickjacking.XFrameOptionsMiddleware :做了clickjacking攻击的保护。clickjacking 保护是攻击者在 自己的病毒网站上，写一个诱惑用户点击的按钮，然后使用iframe的方式将受攻击的网站(比如银行网站)加载到自己的网站 上去，并将其设罝为透明的、用户就看不到、然后再把受攻击的网站(比如银行网站〉的转账按钮定位到病毒网站的按钮上，这 样用户在点击病毒网站上按钮的时候，实际上点击的是受攻击的网站(比如银行网站)上的按钮，从而实现了在不知不觉中给攻击者转账的功能。

## 注意：Django 中间件的排序是有循序的