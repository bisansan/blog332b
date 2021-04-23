---
title: Python的基础语法：编码、标识符和注释
tags: [python]
id: '52'
categories:
  - - 计算机编程
abbrlink: d1a42a19
date: 2018-05-14 15:46:31
---

编码 默认情况下Python uft-8编码作为默认编码，所有字符串都是 unicode 字符串，也可以为源文件直接指定编码 ，字符串的三种指定方式

`# -*- coding:utf-8 -*-`

`# coding=utf-8`

`# -*- coding=utf-8 -*-`

还有一种方式是正规则表达式：`^[ \t\v]``*``#.*?coding[:=][ \t]*([-_.a-zA-Z0-9]+)`

标识符

标识符是程序中有程序员自定义的名称或者符号，如变量名或函数名等等

标识符的组成规则：它可以由数字、下划线和字母组成，标识符是区分大小写，标识符必须以下划线或者字母开头，不能以数字开头

123Ae   A(dd    1&ff     1\_1123aa    aadf-1212

ad123  \_ad123  Ad1233     ad\_eaff123

以下单词不能作为变量名：and as assert break class continue def del elif else except exec finally for from global if in import is lambda not or pass print raise return try while with yield

查看当前版本所有的关键字：

import keyword 

keyword.kwlist 

注释

第一个注释使用

#!/usr/bin/python/

#我是注释

#我可以将字弄消失

#在Coding的时候，我可以作为文字说明

print("hello,world")

当一段话文字太多了，可以这样注释

"""

我是第一行

我是第二行

我是第三行

"""

也可以这样注释

'''

我是第一行

我是第二行

我是第三行

'''