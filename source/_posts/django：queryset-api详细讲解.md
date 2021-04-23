---
title: Django：QuerySet API详细讲解
tags: [django,python]
id: '327'
categories:
  - - 计算机编程
abbrlink: 61c31679
date: 2018-11-30 10:01:09
---

QuerySet API 的对象返回的也是一个QuerySet对象，例如下面的book变量就是一个QuerySet，它可以再次被QuerySet的语法执行

books = Book.objects.filter()
###Book.objects.filter().filter()还可以这样玩哦

filter 过滤