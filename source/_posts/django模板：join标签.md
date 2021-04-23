---
title: Django模板：join、length、lower、random、safe、truncatechars标签
tags: [django,python]
id: '206'
categories:
  - - 计算机编程
abbrlink: 27538b55
date: 2018-10-25 17:01:35
---

join标签类似python的join将指定的列表、元组、字符串拼接起来

text = {
    "akey":\[1,2,3,4\]
}         ###urls.py

{ { akeyjoin:"/" } } #index.html 输出结果为1/2/3/4

length标签获取元组、列表、字符串的长度，类似于python中的len

{ { akeylength } }       ######输出结果为4

lower标签将所有的大写字符转换成小写的形式，upper标签则相反，把所有的小写字母转换成大写

{ { "AAAAA"lower } }     输出结果为aaaaa
{ { "aaaaa"upper } }     输出结果为AAAAA

random标签是随机从字符串、列表、元组中随机获取一个元组

{ { "uqhuqhequ"random } }       输出结果为随机抽取一个

safe标签和autoespace用法差不多，都是关闭默认的转义，对应的字符直接输出

text = {
    "akey":'<script>alert("我是弹窗");</script>'  
}                    ####urls.py
{ { akeysafe } }      #######index.html

  slice标签对字符串进行切片

{ { "gooddd"slice:"0:3" } }    ###输出结果为goo

striptags标签删除字符串里面所有的html标签

text = {
    "akey":'<script>alert("我是弹窗");</script>'
}       ####urls.py

{ { akeystriptags } }     ###index.html输出结果为alert("我是弹窗");

truncatechars标签切割字符串，一般做内容摘要的，用法truncatechars默认加参数时“...”要占用三个字符，所以要用5个字符

{ { "我是一个有长度的字符串"truncatechars:"5" } }    ###输出我是...

truncatechars\_html标签切割字符串，但是它不会把html标签计入字数

text = {
    "akey":"<p>我是一个有长度的字符串</p>"
}

{ { akeytruncatechars\_html:"5" } }     ###输出结果为<p>我是...</p>