---
title: DRF    request视图api
tags: [django,python,Django Rest Framework]
id: '717'
categories:
  - - 计算机编程
abbrlink: 23df9497
date: 2019-08-11 18:44:13
---

request api

request.user 当用户登录时返回当前用户名，没有登录就返回AnonymousUser

request.data 返回用户提交过来的数据，当没有的时候为{}空字典

request.method 返回用户请求的方法

request.query\_params 返回用户提交网址的查询参数，如果没有则为一个空对象