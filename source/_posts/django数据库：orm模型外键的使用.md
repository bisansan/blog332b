---
title: Django数据库：ORM模型外键的使用
tags: []
id: '273'
categories:
  - - Django
date: 2018-11-13 15:40:24
---

如果一张表中有一个非主键的字段指向了别一张表中的主键，就将该字段叫做外键。 district：严格模式(默认), 父表不能删除或更新一个被子表引用的记录。 cascade：级联模式, 父表操作后，子表关联的数据也跟着一起操作。 set null：置空模式,前提外键字段允许为NLL,  父表操作后，子表对应的字段被置空。 DJango使用外键方法使用方法

class Category(models.Model):
    name = models.CharField(max\_length=100)

class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    category = models.ForeignKey('Category',on\_delete=models.CASCADE)###定义一个本模块外键
    author = models.ForeignKey('front.Front',on\_delete=models.CASCADE,null=True)#####定义一个引用其他app目录模块中的外键

同时外键也可以将自己作为外键，这种用途一般作为多级评论

class Comment(models.Model):
    content = models.TextField()
    origin\_comment = models.ForeignKey('self',on\_delete=models.CASCADE)

外键在视图函数中添加值的方法

 article = Article(title='abc',content='111')
 category = Category(name='最新文字')
 category.save()
 article.category = category
 article.save()

在视图函数中调用的方法

def index(request):
    article = Article.objects.first()
    print(article.category.name)

# ![](https://post.332b.com/wp-content/uploads/2018/11/20181113160324.png)一对多的关系示意

向外键的第一个ID添加值进去,下面是models

from django.db import models
class Category(models.Model):
    name = models.CharField(max\_length=100)

class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    category = models.ForeignKey('Category',on\_delete=models.CASCADE,null=True)

视图函数中操作

from django.http import HttpResponse
from .models import Article,Category
def index(request):
    article = Article(title='钢铁是怎样炼成的12121',content='这是一本不错图书，推荐观看和阅读')
    category = Category.objects.first()
    article.category = category
    article.save()
    return HttpResponse("执行成功")

在外键中查看一个外键的值所对应所有值的方法

def index(request):
    category = Category.objects.first()
    article = category.article\_set.all()    ###返回的是一个列表
    for art in article:
        print(art)
    return HttpResponse("执行成功")

将某篇文章添加到某个分类当中方法

def index(request):
    category = Category.objects.first()
    article = Article(title='东方国际很方便',content='ssfsadfsdfds')
    category.article\_set.add(article,bulk=False)
    return HttpResponse("执行成功")

# 一对一的示意方法