---
title: Djiango模板：default、first、floatformat过滤器
tags: []
id: '203'
categories:
  - - Django
date: 2018-10-24 18:04:57
---

default的用法{ {<当前值>:default:<定义的值>} }是当这个值在if中判定为False，例如“”、{}、\[\]、None等等,就会使用它定义的值

{ { valuedefault:"fff" } }    ##输出fff

default\_if\_none的用法{ {<当前值>:default\_if\_none:<定义的值>} }是当这个值为None时就会使用定义的值，例如空列表、空字典等等，用法同上！

{ { valuedefault\_if\_none:"fff" } }    ##输出fff

first和last过滤器的用法分别是取一个列表元组或者字符串的第一个和最后一个元素

{ { valuelast } }   
{ { valuefirst } }

floatformat过滤器的用法{ { valuefloatformat:<数字参数> } }是不加参数默认就保留小数点后面一位数字，有数字参数就按数字参数的次数来保留小数点后面的数 `{ { valuefloatformat:3 } }`