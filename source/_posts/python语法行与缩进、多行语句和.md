---
title: 'Python语法:行与缩进、多行语句、数字类型和字符串'
tags: []
id: '54'
categories:
  - - Python
abbrlink: 7e1b9af4
date: 2018-05-16 11:33:51
---

## 行与缩进

代码块的缩进行数不一致会报错 例如下面正确的： if Ture: print("good") else: print("bad") 错误的格式： if Ture: print("good") else: print("bad")

## **多行语句**

示例一 good = "good\_one" + \\ "good\_two" + \\ "good\_three" + \\ "good\_four" print(good) 输出结果 C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe C:/Users/Administrator/PycharmProjects/untitled/11.py good\_onegood\_twogood\_threegood\_four 进程已结束,退出代码0 示例2 good = ("good\_one","good\_two","good\_three","good\_four") print(good) 输出结果 C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe C:/Users/Administrator/PycharmProjects/untitled/11.py ('good\_one', 'good\_two', 'good\_three', 'good\_four') 进程已结束,退出代码0

## 数字型：

1.int整数，如1 2.bool布尔，如Ture 3.flota浮点数，如1.23、0.12、3E-2 3E-2=3x\[10^(-2)\]=3x\[2/10\]=3x0.2=0.6 4.complex复数如 1 + 2j、 1.1 + 2.2j

## 字符串(String)

python中单引号和双引号使用完全相同。 使用三引号('''或""")可以指定一个多行字符串。 转义符 '\\' 反斜杠可以用来转义，使用r可以让反斜杠不发生转义。。 如 r"this is a line with \\n" 则\\n会显示，并不是换行。 按字面意义级联字符串，如"this " "is " "string"会被自动转换为this is string。 字符串可以用 + 运算符连接在一起，用 \* 运算符重复。 Python 中的字符串有两种索引方式，从左往右以 0 开始，从右往左以 -1 开始。 Python中的字符串不能改变。 Python 没有单独的字符类型，一个字符就是长度为 1 的字符串。 字符串的截取的语法格式如下：变量\[头下标:尾下标\] 输出命令

* * *

str="good123456"
print(str)
print(str\[0\])
print(str\[1\])
print(str\[-2\])
print(str\[3:\])
print(str \* 2)
print(r"hello\\naaa")
print("hello\\naaaa")
print("hello\\'aaaa")

得到数据：

* * *

C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe C:/Users/Administrator/PycharmProjects/untitled/venv/Include/demo.py good123456 g o 5 d123456 good123456good123456 hello\\naaa hello aaaa hello'aaaa 进程已结束,退出代码

* * *

  1、python语法中单双引号使用完全相同 2、python字符串截取字首从0开始，字尾从-1开始 3、python字符串\\n是换行，\\斜杠代表转义，在字符串前面加上“r”,斜杠就可以输出