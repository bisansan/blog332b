---
title: Django：F表达式和Q表达式
tags: []
id: '315'
categories:
  - - Django
date: 2018-11-22 18:01:52
---

F表达式：动态的获取某个字段上的值，并且这个F表达式，不会真正的去数据库中查询数据，他相当于只是起一个标识的作用 F('price')+10表示这个对象里的每个值都要+10，如果是普通命令就要把每个数据拿到内存里然后+10，有了F表达式可以避免这些操作

from django.db.models import F
def index(request):
Book.objects.update(price=F('price')+10)
return HttpResponse('执行成功')

Q表达式：可以实现多个复杂的条件进行查询，它可以执行非（~）、且（&）、或（）这样的查询操作，他的查询条件可以是2个以上，下面是一些代码示例

def index(request):
    books = Book.objects.filter(Q(price\_\_gte=100)  Q(price=95))##查询大于和等于100的价格或者价格等于95
    for book in books:
        print(book.name)
    return HttpResponse('执行成功')

如果我们要查询所有价格不是大于和等于100的数字

books = Book.objects.filter(~Q(price\_\_gte=100))