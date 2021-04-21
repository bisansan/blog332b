---
title: Python3科学计数法，浮点数高精度取法和列表
tags: []
id: '66'
categories:
  - - Python
date: 2018-06-01 17:21:40
---

1.科学计数法1300 = 1.3 x 10^3 = 1.3e3 或者 1.3E3 2.浮点数只能存17位，也就是小数点后16位数，越到后面越不准确，并且在输出的时候的默认会四舍五 3.浮点数高精度取法，使用模块Decimal中的getcontext()来取值

getcontext()=Context(prec=6, rounding=ROUND\_HALF\_EVEN, Emin=-999999, Emax=999999, capitals=1, clamp=0, flags=\[Inexact, Rounded\], traps=\[InvalidOperation, DivisionByZero, Overflow\])

from decimal import \*     ##导入decimal模块## getcontext().prec = 50    ##getcontext设置精度位数## print(Decimal(2) / Decimal(3)) ##打印2除以3的得数## 得到输出结果：0.66666666666666666666666666666666666666666666666667

n = \[1,2,3,4,5,6,7,8,6,4,2,3,4,7,8,3,5,4,4,2,4,3,5,7,7,7,5,\[1,2,3\]\]
print(n\[1\]) ##输出数据列表n第二位数据
print(n\[-1\]\[1\]) ##输出数据列表n子列表中第二位数据
print(n.index(4)) ##输出查询数字4的首个索引值位置
print(n\[n.index(4)\]) ##输出查询数字4的首个索引值位置的数字
s = n.index(4) ##将变量s设置为列表n查询数字4的首个索引值位置值
print(n\[s\])  ##输出它
print(n\[0:3\])  ##输出结果为：\[1, 2, 3\]，输出列表n索引值0—3之间的值，不包含索引值3的值，注意这个是顾头不顾尾
print(n\[:3\])   ##输出结果为：\[1, 2, 3\]，输出列表n索引值0—3之间的值，不包含索引值3的值，注意这个是顾头不顾尾
print(n\[-5:-1\])   ##输出结果为：\[7, 7, 7, 5\]，输出列表n索引值-5—-1之间的值，不包含索引值-1的值，注意这个是顾头不顾尾
print(n\[-5:\])   ##输出结果为：\[7, 7, 7, 5, \[1, 2, 3\]\]，输出列表n索引值-5—-1之间的所有的值
print(n\[::3\])   ##输出结果为：\[1, 4, 7, 4, 4, 3, 4, 3, 7, \[1, 2, 3\]\]，输出列表n所有索引值隔二取一
n2 = \['good','lin','join','oppo'\] 

n2 = \['good','lin','join','oppo'\]
print(n2)
del n2\[2\] ##删除列表n2当中的第三个索引
print(n2)
n2\[2\] = 122  ##修改列表n2当中的第三个索引值为112
print(n2)
print(len(n2))  ##输出列表n2的长度
print(n2 + \["ff","rtttt"\])   ##让两个列表数据相加
print(n2 \* 4)  ##让n2的列表数据重复4遍
print("good" in n2)   ##判断字符串good是否在列表n2里面
for good in n2:       ##如果good字符串在列表n2中，则返回列表n2中的每个值，如果不存在则会报错
    print("单词：",good)
n3 = \[1,2,3,4,5,6,7,8\]
print(max(n3))    ##输出列表n3最大值，如果列表中有字符串则会报错
print(min(n3))    ##输出列表n3最小值，如果列表中有字符串则会报错
n3.append("good")   ##向列表里n3添加一个任意元素，可以是元祖，添加两个则会报错
n3.append(\["lo","pow"\])  ##向列表n3添加两个字符串
n3.extend(\["liyq","opqw"\])  ##entend只能添加列表元素，向列表n3添加两个字符串，注意append和extend的区别
print(n3)