---
title: Django：自带用户管理体系
tags: []
id: '420'
categories:
  - - Django
abbrlink: 5c6810d1
date: 2018-12-29 12:25:22
---

验证和授权概述 Django有一个内置的授权系统。他用来处理用户、分组、权限以及基于cookie的会话系统。Django的授权系统包括验证和授权两 个部分。验证是验证这个用户是否是他声称的人（比如用户名和密码始证，角色验证〉、授权是给与他相应的权限。Django内置的 权限系统包括以下方面：

1.  用户
2.  权限。
3.  分组。
4.  一个可以配置的密码哈希系统，
5.  一个可插拔的后台管理系统。

使用授权系统： 默认中创建完一个django项目后，其实就已经集成了授权系统，那哪些部分是跟授权系统相关的配置呢。以下做一个简单列表： INSTALLED\_APPS : 1. django.contrib.auth :包含了一个核心授权框架，以及大部分的模型定义。 2. django.contrib.contenttypes : Content Type 系统，可以用来关联模型和权限。 中间件 1. SessionMiddleware :用来管理 session 2. AuthenticationMiddieware :用来处理和当前session相关联的用户。   User摸型是这个框架的核心部分。他的完整的路径是在django.contrib.auth.models.User。以下对这个User对象倣一个简单了 解： 字段： 内罝的User模型拥有以下的字段： 1. username :用户名。150个字符以内。可以包含数字和英文字符，以及\_、@、+、.和-字符。不能为空，且必须唯一 2. first\_name :歪果仁的first\_name ,在30;字符以内。可以为空。 3. last\_name :歪果仁的last\_name，在150个字符以内。可以为空。 4. email :邮箱。可以为空。 5. password :密码。经过哈希过后的密码。 6. groups :分组。一个用户可以属于多个分组，一个分组可以拥有多个用户。groups这个字段是跟Group的一个多对多的关 系。 7. user\_permissions :权限。一个用户可以拥有多个权限，一个权限可以被多个用户所有用。和Permission属于一种多对多的关 系。 8. is\_staff :是否可以进入到admin的站点，代表是否是员工。 9. is\_active :是否是可用的。对于一些想要删除账号的数据，我们设晋这个值为False就可以了，而不是真正的从数据库中删 除。 10. is\_superuser :是否是超级管理员。如果是超级管理员，那么拥有整个网站的所有权限。 11 last\_login :上次登录的时间。 12. date\_joined :账号创建的时间。

## 在视图函数中操作账户

1、添加一个普通账户

from django.contrib.auth.models import User
user = User.objects.create\_user(username='a84992',email='1140881@qq.com',password='111111')   # 注册普通账户

2、添加一个管理账户

#user = User.objects.create\_superuser(username='a84991', email='1140882@qq.com', password='111111')   #注册一个管理员账户

3.修改一个账户密码

user = User.objects.get(pk=1)
user.set\_password('111111')
user.save()     #修改密码

4.验证一个账户密码

from django.contrib.auth import authenticate      ##用户验证模块，如果错误返回None

user = 'a84991'
password = '111111'
user = authenticate(request,username=user,password=password)
if user:    ###如果验证成功
    print('登陆成功：%s'% user.username)
else:
    print('用户名或密码错误！')

扩展用户模型。 Django内置的User模型虽然已经足够强大了。但是有时候还是不能满足我们的需求。比如在验证用户登录的时候，他用的是用户名作为验证，而我们有时候需要通过手机号码或者邮箱来进行验证。还有比如我们想要增加一些新的字段。那么这时候我们就雷要扩 展用户模型了。扩展用户摸型有多种方式。这里我们来一一讨论下。 1.设置Proxy模型： 主要是针对User进行代理，只能添加属性，不能添加任何Field字段，否则报错 如果你对Django提供的字段，以及验证的方法都比较满意，没有什么需要改的。但是只是雷要在他原有的基础之上增加一些操作的 方法。那么建议使用这种方式。示例代码如下：

from django.contrib.auth.models import User
class Person(User):
    class Meta:
        proxy = True

    @classmethod              ###classmethod类方法，cls引用类本身
    def get\_blacklist(cls):
        return cls.objects.filter(is\_active=False)

在以上，我们定义了一个Person类，让他继承自User，并且在Meta中设置proxy=True ,说明这个只是User的一个代理模型。 他并不会影响原来User模型在数据库中表的结构。以后如果你想方便的获取所有黑名单的人，那么你就可以通 过Person.get\_blacklist()就可以获取到.并且User.objects.all()和Person.objects.all()其实是等价的。因为他们都是 从User这个模型中获取所有的数据。 2.一对一外键的方式实现User模型的扩展

####models.py
from django.db import models
from django.contrib.auth.models import User
from django.dispatch import receiver     #监听模块
from django.db.models.signals import post\_save   #数据保存后通知模块
class UserExtension(models.Model):
    user = models.OneToOneField(User,on\_delete=models.CASCADE,related\_name='extension')
    telephone = models.CharField(max\_length=11)
    school = models.CharField(max\_length=100)

@receiver(post\_save,sender=User)
def handler\_user\_extension(sender,instance,created,\*\*kwargs):  #sender发送者，instance实例User在保存时候的对象，created是否是新创建，user是上面UserExtension中的user
    if created:
        UserExtension.objects.create(user=instance)
    else:
        instance.extension.save()

在视图中操作的方法

from django.http import HttpResponse
from django.contrib.auth.models import Userdef one\_view(request):
    user = User.objects.create\_user(username='zhiliao3',email='2115445@qq.com',password='111111')
    user.extension.telephone = '11111441111'
    user.save()
    return HttpResponse('one to one')

如果需要使用验证用户手机号和密码，可以在视图中这样操作

def my\_authenticate(tetephone,password):
    user = User.objects.filter(tetephone=tetephone).first()
    if user:
        is\_correct = user.check\_password(password)
        if is\_correct:
            return user
        else:
            None
    else:
        None
def verify(request):
    telephone = request.POST.get('telephone')
    password = request.POST.get('password')
    user = my\_authenticate(telephone,password)
    if user:
        print('验证成功')
    else:
        print('验证失败')

3.修改继承类AbstractUser，重新定义User，AbstractUser是User的父类 一、改变USER的结构，在USER里面直接添加字段 定义User首先在setting.py中添加制定用户模型，不用写成front.models.User，它会自动识别

AUTH\_USER\_MODEL = 'front.User'

我们先来继承User所有的字段，定义新的字段或者直接覆盖原来的字段，USERNAME\_FIELD制定新的验证字段为手机号，而不是原来的username

from django.contrib.auth.models import AbstractUser,UserManager

class User(AbstractUser):
    telephone = models.CharField(max\_length=11,unique=True)
    school = models.CharField(max\_length=100)
    USERNAME\_FIELD = 'telephone'

BaseUserManager定义保存属性，由于它默认定义的是username，我们要将它更改为手机号，所以也需要重新定义

class UserMangen(BaseUserManager):
    def \_create\_user(self,telephone,username,password,\*\*kwargs):   #下划线开头为私有变量，只能在这个类里面使用
        if not telephone:
            raise ValueError('必须要传递一个手机号')
        if not password:
            raise ValueError('必须要输入密码')
        user = self.model(telephone=telephone,username=username,password=password,\*\*kwargs)
        user.set\_password(password)
        user.save()
        return user

    def create\_user(self,telephone,username,password,\*\*kwargs):
        kwargs\['is\_superuser'\] = False
        return self.\_create\_user(telephone=telephone,username=username,password=password,\*\*kwargs)

    def create\_superuser(self,telephone,username,password,\*\*kwargs):
        kwargs\['is\_superuser'\] = True
        return self.\_create\_user(telephone=telephone, username=username, password=password,\*\*kwargs)

如果我们需要在视图中添加数据，就可以这样操作，如果要验证用户和密码，参考上面的‘’验证一个账户密码‘’，注意user是一个手机号，不再是一个用户名，authenticate(request,username=user,password=password)

from .models import User
from django.http import HttpResponse

def one(request):
    telephone = '18894148309'
    password = '111111'
    username = 'zhiloiao'
    user = User.objects.create\_user(telephone=telephone,username=username,password=password)
    print(user.username)
    return  HttpResponse('index')

二、直接自定义USER的所有的字段 setting.py里面的AUTH\_USER\_MODEL = 'front.User'不能少，下面是models.py的内容，如果要自己定义USER模型，那么必须在第一次运行migrate命令之前先创建好模型

from django.db import models
from django.contrib.auth.models import BaseUserManager,PermissionsMixin,UserManager
from django.contrib.auth.base\_user import AbstractBaseUser

class UserMangen(BaseUserManager):
    def \_create\_user(self,telephone,username,password,\*\*kwargs):   #下划线开头为私有变量，只能在这个类里面使用
        if not telephone:
            raise ValueError('必须要传递一个手机号')
        if not password:
            raise ValueError('必须要输入密码')
        user = self.model(telephone=telephone,username=username,password=password,\*\*kwargs)
        user.set\_password(password)
        user.save()
        return user

    def create\_user(self,telephone,username,password,\*\*kwargs):
        kwargs\['is\_superuser'\] = False
        return self.\_create\_user(telephone=telephone,username=username,password=password,\*\*kwargs)

    def create\_superuser(self,telephone,username,password,\*\*kwargs):
        kwargs\['is\_superuser'\] = True
        return self.\_create\_user(telephone=telephone, username=username, password=password,\*\*kwargs)

class User(AbstractBaseUser,PermissionsMixin):     #PermissionsMixin为用户权限验证功能
    telephone = models.CharField(max\_length=11,unique=True)
    email = models.CharField(max\_length=100,unique=True)
    username = models.CharField(max\_length=100)
    is\_active = models.BooleanField(default=True)

    USERNAME\_FIELD = 'telephone'
    REQUIRED\_FIELDS = \[\]

    objects = UserManager()

    def get\_full\_name(self):
        return self.username
    def get\_short\_name(self):
        return self.username

在views.py里面的字段，添加用户数据

from django.http import HttpResponse
from .models import User
def index(request):
    sd = User.objects.create\_user(telephone='18894148319',username='zhil1ao',email='1111@qq.com',password='1111111')
    # sd.set\_password('1111111')
    # sd.save()
    return HttpResponse('index')

我们可以用一个模块读取setting.py设置AUTH\_USER\_MODEL中的制定的User模型，这样就方便我们动态的去修改

from django.contrib.auth import get\_user\_model
class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    author = models.ForeignKey(get\_user\_model(),on\_delete=models.CASCADE)

权限和分组 登录、登录限制和注销，下面是代码演示下载，[login\_and\_logout.zip](https://post.332b.com/wp-content/uploads/2018/12/login_and_logout.zip) 登录from django.contrib.auth import login 使用方法

def my\_login(request):    ###千万不要直接用login函数，否则会跟django自带的函数冲突
    if request.method == 'GET':
        return render(request,'login.html')
    else:
        form = Loginform(request.POST)
        if form.is\_valid():
            telephone = form.cleaned\_data.get('telephone')
            password = form.cleaned\_data.get('password')
            remember = form.cleaned\_data.get('remember')
            user = authenticate(request,username=telephone,password=password)
            if user and user.is\_active:
                login(request,user)
                if remember:
                    request.session.set\_expiry(None)    #session两周过期
                    return HttpResponse('登录成功')
                else:
                    request.session.set\_expiry(0)   #session浏览器关闭就过期
                    next = request.GET.get('next')
                    if next:
                        return redirect(next)         ###如果有传入来源url参数，登录成功就跳转到该URL
                    else:
                        return HttpResponse('登录成功')
            else:
                #print(form.errors)
                return HttpResponse('手机号或者密码错误')
        else:
            print(form.errors)
            return redirect(reverse('login'))

注销from django.contrib.auth import logout使用方法

def my\_logout(request):
    logout(request)
    return HttpResponse('注销成功')

登录限时模块的示例 from django.contrib.auth.decorators import login\_required ##验证用的模块户是否登录

@login\_required(login\_url=r'/login/')   ###不指定login\_url默认会跳转到accounts/login/?next=/view/
def logineded\_view(request):
    return HttpResponse('个人中心，只有登录才能查看')