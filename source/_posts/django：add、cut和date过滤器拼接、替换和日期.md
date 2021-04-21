---
title: Django：add、cut和date过滤器拼接、替换和日期
tags: []
id: '201'
categories:
  - - Django
abbrlink: 79e67bf9
date: 2018-10-24 17:13:06
---

因为Django中DTL是不支持给函数传参数的，所以就出现了过滤器，add过滤器的用法<参数1>add:<参数2>，当参数1和参数2是数字就会相加，如果都是列表或者字符串就会拼接

{ { "1"add:"12" } }  ###13

cut过滤器是将指定字符删掉，用法如下

{ { "good"cut:"d" } }    ###goo

date过滤器，是格式化字符串成为自己想要的模式

text = {
    "seer":datetime.now()
}                       ####urls.py

{ { seerdate:"Y-m-d" } }   ####index.html 输入当前时间为“2018-10-24”这种格式