---
title: Django：聚合函数
tags: []
id: '290'
categories:
  - - Django
abbrlink: 7c2366e
date: 2018-11-21 18:05:28
---

  1.所有的聚合函数都在'django.db.models'下面

#### Avg为统计所对应的id所有值的平均值

2.聚合函数不能单独的执行，需要放在一些可以执行聚合函数的方法下面去执行，比如‘aggregate’，示例代码

from django.http import HttpResponse
from .models import Book
from django.db.models import Avg
from django.db import connection
def index(request):
    result = Book.objects.aggregate(Avg("price"))
    print(result)
    print(connection.queries)
    return HttpResponse('执行成功')

执行之后 `{'price__avg': 94.75}` `[21/Nov/2018 16:06:38] "GET / HTTP/1.1" 200 12` ``[{'sql': 'SELECT @@SQL_AUTO_IS_NULL', 'time': '0.024'}, {'sql': 'SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED', 'time': '0.024'}, {'sql': 'SELECT AVG(`book`.`price`) AS `price__avg` FROM `book`', 'time': '0.024'}]`` 聚合函数执行完成后，给这个聚合函数的值取个名字。取名字的规则，默认就是‘filed+\_+聚合函数的名字’，例如上面的`'price__avg'` price为Book模型中的price，avg为集合函数名字，如果不想使用这样的名字，可以给聚合函数传递关键字参数，参数的名字就是聚合函数执行完成的名字，代码如下

result = Book.objects.aggregate(avgst = Avg("price"))

aggregate：返回的不是一个QuerySet对象，它返回的是一个字典，这个字典的key就是集合函数的名字，值就是执行后的结果 查看不是QuerySet的对象，执行的原生SQL语句可以用`connection.queries` "annotate"和"aggregate"不同的地方是，他返回的是一个QuerySet对象，而不是一个字典 相同的地方是两个方法可以执行聚合函数，不同的是"annotate"返回的是QuerySet对象，并且会在查找的模型上添加一个聚合函数的属性，"aggregate"不会对数据进行分组，它会求所有值的平均数，"annotate"会使用SQL语法group by按分组的数字进行求每一条数据的平均值。 Count统计所对应的id的单位总数，它有一个属性distinct=True可以剔除所有的重复的值

def index(request):
    books = Book.objects.annotate(book\_sunms = Count("bookorder",distinct=True))
    for book in books:
        print('%s/%s'% (book.name,book.book\_sunms))
    return HttpResponse('执行成功')

Min统计所对应的对象中最小的值，Max则是最大的值

def index(request):
    result = Author.objects.aggregate(max=Max('age'),min=Min('age'))
    print(result)
    return HttpResponse('执行成功')

Sum统计所对应的对象中所有值相加的和

def index(request):
    result = Author.objects.aggregate(min=Sum('age'))
    print(result)
    return HttpResponse('执行成功')

提取2018年所有的图书的销售总额方法

def index(request):
    result = BookOrder.objects.filter(create\_time\_\_year=2018).aggregate(total=Sum('price'))
    print(result)
    return HttpResponse('执行成功')

‘aggregate’和"annotate"可以使用在任何QuerySet对象上使用 如果要统计2018年，每一本图书的价格，代码如下

def index(request):
    books = Book.objects.filter(bookorder\_\_create\_time\_\_year=2018).annotate(total=Sum('bookorder\_\_price'))
    for book in books:
        print('%s/%s'% (book.name,book.total))
    return HttpResponse('执行成功')

[聚合函数](https://post.332b.com/wp-content/uploads/2018/11/聚合函数.zip)