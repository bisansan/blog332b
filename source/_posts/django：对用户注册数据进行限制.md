---
title: Django：对用户注册数据进行限制
tags: []
id: '385'
categories:
  - - Django
abbrlink: 98c3e256
date: 2018-12-12 14:46:21
---

下面代码实现一个简单的验证，主要作用 1.对输入的手机号检查是否是唯一的手机号 2.对输入的两次密码进行验证 forms.py  表单

from django import forms
from django.core import validators
from .models import User
class Index(forms.Form):
    user = forms.CharField(max\_length=10)
    tel = forms.CharField(validators=\[validators.RegexValidator(r'1\[3456789\]\\d{9}',message='手机号码格式错误')\])
    pwd1 = forms.CharField(max\_length=16,min\_length=6)
    pwd2 = forms.CharField(max\_length=16, min\_length=6)

    def clean\_tel(self):
        tel = self.cleaned\_data.get('tel')  ###可以对tel字段进行二次验证,优先执行本段，然后去执行视图函数中的字段
        exists = User.objects.filter(tel=tel).exists()   ###查找是否有相同字段
        if exists:
            raise forms.ValidationError(message='tel验证失败，因为已经存在了') ###抛出异常，停止执行
        return tel

    def clean(self):
        cleaned\_data = super().clean()
        pwd1 = cleaned\_data.get('pwd1')
        pwd2 = cleaned\_data.get('pwd2')
        if pwd1 != pwd2:
            raise forms.ValidationError(message='两次密码不一样')
        else:
            return cleaned\_data

views.py文件

from django.views.generic import View
from django.shortcuts import render
from .models import User
from .froms import Index
from django.http import HttpResponse
class Index1(View):
    def get(self,request):
        return render(request,'io.html')
    def post(self,request):
        form = Index(request.POST)
        if form.is\_valid():
            print('good2')
            user1 = form.cleaned\_data.get('user')  ###提取已经验证过的数据
            tel1 = form.cleaned\_data.get('tel')
            User.objects.create(user=user1,tel=tel1)
            return HttpResponse('执行成功')
        else:
            print(form.errors.get\_json\_data())
            return HttpResponse('执行失败')

models.py

from django.db import models

class User(models.Model):
    user = models.CharField(max\_length=10)
    tel = models.CharField(max\_length=11)

index.html模板

<form action="" method="post">
    <table>
        <tr>
            <td>用户名:</td>
            <td><input type="text" name="user"></td>
        </tr>
        <tr>
            <td>手机号：</td>
            <td><input type="text" name="tel"></td>
        </tr>
        <tr>
            <td>密码1：</td>
            <td><input type="password" name="pwd1"></td>
        </tr>
        <tr>
            <td>密码2：</td>
            <td><input type="password" name="pwd2"></td>
        </tr>
        <tr>
            <td></td>
            <td><input type="submit" value="提交"></td>
        </tr>
    </table>
</form>

用户名和密码 froms.py

from django import forms
from django.core import validators
from .models import Book,User

class AddBookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = '\_\_all\_\_'
        #fields = \['title','page'\]
        #exclude = \['price'\]
        error\_messages = {
            'page':{
                'required':'请传入page参数',
                'invalid':'请输入一个可用的page参数'
            },
            'title':{
                'max\_length':'title不能超过100字符'
            },
            'price':{
                'max\_value':'最大不能超过100元'
            }

        }
class Reg(forms.ModelForm):
    pw1 = forms.CharField(max\_length=16,min\_length=6)
    pw2 = forms.CharField(max\_length=16,min\_length=6)
    def clean(self):
        cleaned\_data = super().clean()    ###调用自身重写clean
        pw1 = cleaned\_data.get('pw1')
        pw2 = cleaned\_data.get('pw2')
        if pw1 != pw2:
            raise forms.ValidationError(message='密码两次输入不一致哦')
        return cleaned\_data
    class Meta:
        model = User
        exclude = \['password'\]

models.py

from django.db import models
from django.core import validators
class Book(models.Model):
    title = models.CharField(max\_length=100)
    page = models.IntegerField()
    price = models.FloatField(validators=\[validators.MaxValueValidator(limit\_value=100)\])

class User(models.Model):
    username = models.CharField(max\_length=100)
    password = models.CharField(max\_length=16)
    telephone = models.CharField(max\_length=11)
# Create your models here.

views.py

from django.shortcuts import render
from django.views.generic import View
from django.shortcuts import render
from .models import User
#from .froms import Index
#from .froms import AddBookForm
from django.views.decorators.http import require\_POST
from .forms import AddBookForm,Reg
from django.http import HttpResponse
from django import forms
def index(request):
    return HttpResponse('执行首页')
def add\_book(request):
    form = AddBookForm(request.POST)
    if form.is\_valid():
        # title = form.cleaned\_data.get('title')
        # page = form.cleaned\_data.get('page')
        # price = form.cleaned\_data.get('price')
        # print('title:%s'% title)
        # print('page:%s' % page)
        # print('price:%s'% price)
        form.save()
        return HttpResponse('执行成功')
    else:
        print(form.errors.get\_json\_data())
        return HttpResponse('执行失败')

@require\_POST
def reg(request):
    form = Reg(request.POST)
    if form.is\_valid():
        user = form.save(commit=False)
        user.password = form.cleaned\_data.get('pw1')
        user.save()
        return HttpResponse('注册成功')
    else:
        print(form.errors.get\_json\_data())
        return HttpResponse('注册失败')

  3       3