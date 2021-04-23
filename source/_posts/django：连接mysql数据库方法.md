---
title: Django：连接mysql数据库方法
tags: [django,python,mysql]
id: '238'
categories:
  - - 计算机编程
abbrlink: 2455b3ee
date: 2018-11-08 10:08:06
---

在settting.py修改如下成,Django会自动识别数据库连接件，常见的连接间有pymysql(Py语言编写)、mysqlclient(C语言编写)

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'db\_name',
        'USER':'user',
        'PASSWORD':'password',
        'HOST':'localhost',
        'PORT':'3306',
    }
}

在视图函数中的引用方法是

def index(request):
    cursor = connection.cursor()       ###获取游标
    cursor.execute("select id,name,author from book")    ####从book表中查找id,name,author字段，如果是\*代表所有

#    cursor.execute("insert into book(id,name,author) values(null,'三国演义','罗贯中')")   ####这个代表插入，id设置null是因为数据库设置了自动递减

    rows = cursor.fetchall() return render(request,"index.html",context={"books":rows})

在模板中输出的方法

{ % for fo in books %}
 <td>{ {fo} }</td>
{ % endfor %}