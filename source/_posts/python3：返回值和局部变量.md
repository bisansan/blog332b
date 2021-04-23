---
title: Python3：返回值、局部变量、作用域、匿名函数
tags: [python]
id: '111'
categories:
  - - 计算机编程
abbrlink: aa498e1f
date: 2018-09-17 16:32:27
---

def name1(a,b):
    if a > b :
        a / b
        return True
    else:
        a \* b
        return False
 print(a,b)
    print("abc")
print(name1(32,8))

return可以返回任何值，他可以是一个变量、字符串或者列表等等，当需要返回多个值时，它默认是以元祖的的形式返回，当return没有返回值时，它默认会返回一个None,一个函数只要执行了一次return就代表当前函数终止，不会再执行当前函数的其他命令，例如print(a,b)和print("abc") 都不会再执行了。

x1 = '你好，孩子！'
x2 = \[1,2,3,4,5,6\]
def name1():
    global x1
    print(x1)
    x1 = "你好，世界!"
    print(x1)
    del x2\[2\]
    print(x2)
name1()
print(x1,x2)

局部变量是指函数里面的变量，在函数里查找变量是由内向外查找，有局部变量就优先使用，没有就向外查找全局变量，在函数里面无法修改全局变量，但如果全局变量是一个列表，那么在函数里，无法修改全部变量的整个列表，但可以修改列表里面的每一个元素。global x1的用法是将全局变量引入到函数来变为可修改。

n1 = 18
def a1():
    n1 = 19
    print('good')
    def a2():
        print(n1)
    return a2
print(a1())
a3 = a1()
print(a3())
print(n1)

作用域是指代码已经生成作用域已经生成，作用域链向上查找，返回值可以是函数例如return a2，函数也是一个作用域，函数里面镶入一个函数饺子镶套函数，无论是函数里面镶入多少个函数，它的执行永远都是由里到外，查找变量也是由里到外；

s = lambda x,y:x\*3 if x>y else x/y
print(s(6,3))
k = (list(range(1,10)))
def n(x):
    return x \*\* 3
print(list(map(n,k)))
print(list(map(lambda x:x\*\*3,k))
print(abs(-100))

匿名函数lambda支持简单明了的语句，最大能支持三元运算，它最大的作用是配合其他的语法进行使用，map()函数的基本用法是一个函数接一个列表，它会用函数来遍历列表的每一个元素，abs代表求绝对值，无论正负都会转换成正数