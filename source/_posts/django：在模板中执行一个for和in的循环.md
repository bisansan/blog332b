---
title: Django：在模板中执行for...in的循环和列表显示文字
tags: [django,python]
id: '182'
categories:
  - - 计算机编程
abbrlink: 8c1091f5
date: 2018-10-23 17:03:38
---

1.在django模板当中reversed可以将for循环的结果倒序显示，用for循环字典，有三个语法items(取key和值)、keys（去所有的key）、values（取所有的值） 2.`forloop.counter` 从1开始获取当前循环次数，如果是`forloop.counter0` 则代表从0开始,`forloop.revcounter` 跟`forloop.counter` 得到的结果相反，用法一样 `forloop.first` 判断一个循环次数是否在第一次 `forloop.last` 判断一个循环次数是否在最后一次 `forloop.parentloop` 未知 3.除了for...in以外，还有一个for...in...empty跟for...in使用方法一样，for循环没有任何值的时候，它就会执行empty里面的语法，empty一般用在评论里面，假如没有评论就显示empty里面的语法“当前没有任何评论”，如果有就执行for...in...遍历评论 urls.py文件

from django.urls import path
from django.shortcuts import render

def index(request):
    return render(request,"index.html",context=text)
text ={
    "danchi":\["三国","日本","土匪","输入法","苹果皮"\],
    "book":\[
        {"name":"三国演义",
         "author":"罗贯中",
         "price":99},
        {"name":"水浒传",
         "author":"施耐庵",
         "price":80
         },
        {"name":"西游记",
         "author":"罗贯中",
         "price":89}\]
}

urlpatterns = \[
    path('admin/', admin.site.urls),
    path("",index)
\]

index.html文件

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<ul>
    { % for foo in danchi reversed %}
        <li>{ { foo } }</li>
    { % endfor %}
</ul>
{ % for b1,b2 in book.0.items %}
<li>{ { b1 } }/{ { b2 } }</li>
{ % endfor %}
<table>
    <thead>
        <tr>
            <td>序号</td>
            <td>书面</td>
            <td>作者</td>
            <td>价格</td>
        </tr>
    </thead>
    <tbody>
        { % for b3 in book %}
                { % if forloop.parentloop %}
                    <tr style="background: red;">
                { % elif forloop.last %}
                    <tr style="background: aquamarine;">
                { % else %}
                    <tr>
                { % endif %}
                <td>{ { forloop.revcounter } }</td>
                <td>{ { b3.name } }</td>
                <td>{ { b3.author } }</td>
                <td>{ { b3.price } }</td>
            </tr>

        { % endfor %}

    </tbody>
</table>

</body>
</html>

![](https://post.332b.com/wp-content/uploads/2018/10/20181023170213-256x300.png)