---
title: Django笔记：虚拟环境和URL视图参数
tags: []
id: '145'
categories:
  - - Django
abbrlink: cf74a71f
date: 2018-10-16 16:10:47
---

1.虚拟环境安装：`pip install virtualenv` 创建virtualenv虚拟环境:`virtualenv [目录路径]` 进入虚拟环境Scripts目录或者bin目录执行`activate`命令，`deactivate`退出虚拟环境 2.高级虚拟环境virtualenvwrapper安装，Windows安装`pip install virtualenvwrapper-win` 创建virtualenv虚拟环境:`mkvirtualenv [目录路径]` 3.创建第一个Django项目：`django-admin startproject first_project` 4.启动Diango项目：`python manage.py runserver` 可选参数可加上本机IP地址:端口号，默认以8000端口启动，注意要修改setting.py里面的ALLOWED\_HOSTS = \[\]填入本机IP，否则其他机器无法访问 5.项目路径URL映射文件urls.py，URL规则如下

from django.urls import path
from django.http import HttpResponse

def index(request):
    return HttpResponse("首页")

def book(request):
    return HttpResponse("书城")

urlpatterns = \[
    path("",index),
    #这个是首页
    path("book/",book)
    #这个是/book路径
\]

6.创建一个项目app目录`python manage.py startapp [名称]`，DEBUG默认是开启的，它可以显示我们开发中出现错误的地方，在生产环境必须关掉DEBUG模式 7.在pycharm鼠标选择模块代码，快捷键Ctrl + B可以进入模块的目录文件 8.视图函数的第一个参数必须是request,视图函数的返回值必须是django.http.response.HttpResponseBase的子类 9.Django的URL映射配置是先到settting.py中寻找`ROOT_URLCONF = 'untitled.urls'`  所配置的值，然后再去url.py寻找所对应的URL关系 10.URL传参数在url.py中的path()中可以用<参数>的方式来传参数 url.py文件中的部分

path("book/detail\_<book\_id>.html",views.book\_detail)
#域名www.xxx.com/book/detail\_xxx.html

views.py文件中的部分

def book\_detail(request,book\_id):
    text = "你的ID是：%s" % book\_id
    return HttpResponse(text)

11.查询字符串GET的方式传参数，他的参数是request.GET.get("参数"),这个数据获取的方式get类似于字典，所获取的值也跟字典类似 url.py文件中的部分

path("book/author",views.author\_detail)
#域名www.xxx.com/book/author?id=xxx

views.py文件中的部分

def author\_detail(request):
    author\_id = request.GET.get("id")
    author\_text = "作者ID是：%s" % author\_id
    return HttpResponse(author\_text)

12.URL转换器共有5种类型，他可以为URL制定数据类型，可以例如url中的这段代码path("book/detail\_<str:book\_id>.html",views.book\_detail)，str:指定的是字符串类型，模块的命令是`from django.urls import converters` str:   除了“/”不行，其他都可以输入 int:  只能为纯数字 path:  可以为任意字符 uuid:  只能满足python自带模块uuid中的uuid.uuid4()的类型 slug:  阿拉伯数字和字母，英文中的横杠和下划线 13.让url映射可以在多个app的urls.py中配置的方法，主项目中的urls.py指定各app中的urls路径 主项目urls.py文件：

from django.urls import path,include

urlpatterns = \[
    path("book/", include('book.urls')),
\]

book单个app目录urls.py

from django.urls import path
from . import views

urlpatterns = \[
    path("", views.index),
    path("denglu/",views.login)
\]

为一个URL指定名称在urls.py文件修改path，就相当于给url制定了一个login变量名称，singup则为login变量的值，app命令空间是为了防止各个app之间相同的反转URL变混淆，添加方法在urls.py中添加app\_name = "应用空间名称" app目录urls.py的部分代码示例

app\_name = "xlogin"

path("singup/",views.login,name="login")

在views.py使用方法：

rom django.http import HttpResponse
from django.shortcuts import redirect,reverse

def index(request):
    username = request.GET.get("username")
    if username:
        return HttpResponse("前台首页")
    else:
        login\_url = reverse("xlogin:login")
        return redirect(login\_url)

def login(request):
    return HttpResponse("前台登陆页面")

14.当一个app在总项目中的urls.py只指定一个URL叫做应用命名空间，当多个URL指向同一个app，多个URL之间URL反转会混淆，为了避免这种情况，可以使用实例命名空间 主项目urls.py的配置，在urls.py中配置namespace="名称"

from django.urls import path,include

urlpatterns = \[
    path("", include('login.url')),
    path("book/", include('book.url',namespace="book"),),
    path("book1/", include('book.url',namespace="book1")),
\]

在app目录中配置views.py使用request.resolver\_match.namespace来获取当前执行的命名空间避免混淆

def index(request):
    username = request.GET.get("username")
    if username:
        return HttpResponse("书城首页")
    else:
        current\_namespace = request.resolver\_match.namespace
        login\_url = reverse("%s:login"%current\_namespace)
        return redirect(login\_url)
def login(request):
    return HttpResponse("书城登陆页面")

要想使用实例命令空间，就必须要先指定应用命令空间，也就是在当前app目录中指定app\_name = "名称" 15.文件urls.py中的include()函数用法 include(module,namespace=None) `path("book/", include('book.url',namespace="book"),)` include((pattern\_list,app\_namespace),namespace=None) `path("book/", include('book.url',"book"))` include(pattern\_list):

path("book/", include(\[
    path("",views.book),
    path("list/",views.booklist)
\])),