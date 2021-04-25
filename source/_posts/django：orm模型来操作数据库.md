---
title: Django：ORM模型来操作数据库
tags: [Django,python]
id: '252'
categories:
  - - 计算机编程
abbrlink: 8d6e45cc
date: 2018-11-11 20:41:16
---

ORM模型更方便我们来操作数据库，原生的SQL容易遭到攻击，ORM模型就可以尽可能的去避免这些事情的发生，经测试使用后性能损失不到5% 下面是已经创建了一个book的app，建好了数据库连接，已经将book安装到了setting.py里去了，下面这个对应的是book的models.py文件

from django.db import models
class book(models.Model):
    id = models.AutoField(primary\_key=True)    ##将id设置成自动增涨，并设置为关键key
    name = models.CharField(max\_length=100,null=False)   ###将name设置为字符串，长度为100个字符，null不能为空
    author = models.CharField(max\_length=100,null=False)   ###同上
    price = models.FloatField(null=False,default=0)    ##将price设置为浮点数，null不能为空，如果没有值默认是0

下面生成迁移脚本和建立数据库连接关系

manage.py makemigrations ##生成迁移脚本
manage.py migrate ###映射数据库关系

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2018/11/20181111174010.png) 如果你没有写数据库名字，那么他创建的数据库表就是，就是book\_book（app的名字+class的名字），下面图片就是刚刚创建的 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2018/11/20181111175828.png) 猜猜这段代码什么意思？要不要自己动手试试效果

def \_\_str\_\_(self):
    return "<Book:({name},{author},{price})>".format(name=self.name,author=self.author,price=self.price)

一些在视图函数views.py中操作CRM增删改查的方法

from .models import Book    ##先载入一下ORM模块
from django.http import HttpResponse
def index(requset):
    #一、增加数据
    # book = Book(name='西游记',author='吴晨歌',price='501')
    # book.save()
    #二、查询数据  1.通过主键key来查找   2.根据其他条件查询
    # book = Book.objects.get(pk=1)  ##get=只查找一条，通过key来查询，pk为primary key的缩写
    # print(book)
    # book = Book.objects.filter(name='西游记') ###通过其他条件查询，返回的是一个所有包含这个值的列表，可以在后面加个.first来获取第一个值
    # print(book)
    #三、删除数据
    # book = Book.objects.get(pk=1)  ##通过get到key之后，再进行删除
    # book.delete()
    #四、更改数据
    # book = Book.objects.get(pk=2)  ##先get到key，再直接通过属性进行修改
    # book.price = 2000
    # book.save()
    return HttpResponse("书籍操作")

# 关于一些ORM数据类型的标签的含义

一、在CRM中定义一个主键，就必须要设置(primary\_key=True)

#### AutoField

将值设置为任意值自动增涨，-1、0、1、2、3............

#### BigAutoField

将值设置为从1开始自动增涨，它是64位整形

#### Booleanfield 和 NullBooleanfield

从模板层接受True/False，存到数据为tinyint类，存储的时候就是1和0，不能为空null并且这个数据必须设置一个默认值，NullBooleanfield就可以为null

#### CharField

是将值以字符串的形式存在数据库，它必须用max\_length=100来设置最多长度，如果文字太多，就建议使用longText类型

#### DateTimeField、TimeField和DateField

这是那个分别可以在数据库存日期和时间、时间和日期

#### EmailFaild

存储邮件字符串，他的长度最大为254个，它也可以是纯文本，他 CharField 文本字符串，最大只能255个字符

#### FloatField

浮点数类型

#### IntegerField

整形，值的区间负10位到正10位之间的所有数字

#### BigIntegerField

大整形，值的区间负19位到正19位之间的所有数字

#### PostIntegerField

正整型，值区间为0到正十位数之间

#### SmallIntegerField

小整形，值的区间是-32760-32767

#### PositiveSmallIntegerField

正小整形，值的区间0-32767

#### TextField

大量文本类型，映射数据库中的longtext类型

#### UUIDField

只能存储uuid格式的字符串，uuid是一个32位的全球唯一的字符串，一般作为主键

#### URLField

类似charfiled，只不过只能存储url格式的字符串，并且默认max\_length是200

# 关于一些ORM数据类型的参数的含义

null null代表空值，默认情况下代表它是False，不能为空值，空值不等于空字符串 blank 表示这个字段是否可以在表单中可以为空，默认情况下代表它是False，它是表单级别的，null是数据库级别的 db\_column 这个字段可以设置数据库的名字，如果没有这个参数，那么将会使用模型中的属性名字 default 为字段设置一个默认的值，它除了可以是一个值以外还可以是一个函数，注意是函数，而不是一个函数的返回值（就是不加括号的函数） unique 在表这个字段中的值是否是唯一的值，一般是来设置手机号/邮箱，可以和null配合使用 primary\_key 是否为主键，默认不是