---
title: Python3模块：随机取数random模块
tags: []
id: '142'
categories:
  - - Python
date: 2018-10-11 14:32:17
---

程序中有很多地方需要用到随机字符，比如登录网站的随机验证码，通过random模块可以很容易生成随机字符串

```
>>> random.randrange(1,10) #返回1-10之间的一个随机数，不包括10
>>> random.randint(1,10) #返回1-10之间的一个随机数，包括10

>>> random.randrange(0, 100, 2) #随机选取0到100间的偶数

>>> random.random()  #返回一个随机浮点数
>>> random.choice('abce3#$@1') #返回一个给定数据集合中的随机字符
'#'

>>> random.sample('abcdefghij',3)  #从多个字符中选取特定数量的字符
['a', 'd', 'b']

#生成随机字符串
>>> import string 
>>> ''.join(random.sample(string.ascii_lowercase + string.digits, 6)) 
'4fvda1'

#洗牌
>>> a
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> random.shuffle(a)
>>> a
[3, 0, 7, 2, 1, 6, 5, 8, 9, 4]
```

**random.random** random.random()用于生成一个0到1的随机符点数: 0 <= n < 1.0 **random.uniform** random.uniform(a, b)，用于生成一个指定范围内的随机符点数，两个参数其中一个是上限，一个是下限。如果a > b，则生成的随机数n: a <= n <= b。如果 a <b， 则 b <= n <= a

代码如下:

print random.uniform(10, 20) print random.uniform(20, 10) # 18.7356606526 # 12.5798298022

  **random.randint** random.randint(a, b)，用于生成一个指定范围内的整数。其中参数a是下限，参数b是上限，生成的随机数n: a <= n <= b

代码如下:

print random.randint(12, 20)  # 生成的随机数 n: 12 <= n <= 20 print random.randint(20, 20)  # 结果永远是20 # print random.randint(20, 10)  # 该语句是错误的。下限必须小于上限

  **random.randrange** random.randrange(\[start\], stop\[, step\])，从指定范围内，按指定基数递增的集合中 获取一个随机数。如：random.randrange(10, 100, 2)，结果相当于从\[10, 12, 14, 16, ... 96, 98\]序列中获取一个随机数。random.randrange(10, 100, 2)在结果上与 random.choice(range(10, 100, 2) 等效 **random.choice** random.choice从序列中获取一个随机元素。其函数原型为：random.choice(sequence)。参数sequence表示一个有序类型。这里要说明 一下：sequence在python不是一种特定的类型，而是泛指一系列的类型。list, tuple, 字符串都属于sequence。有关sequence可以查看python手册数据模型这一章。下面是使用choice的一些例子：

代码如下:

print random.choice("学习Python") print random.choice(\["JGood", "is", "a", "handsome", "boy"\]) print random.choice(("Tuple", "List", "Dict"))

  **random.shuffle** random.shuffle(x\[, random\])，用于将一个列表中的元素打乱。如:

代码如下:

p = \["Python", "is", "powerful", "simple", "and so on..."\] random.shuffle(p) print p # \['powerful', 'simple', 'is', 'Python', 'and so on...'\]

  **random.sample** random.sample(sequence, k)，从指定序列中随机获取指定长度的片断。sample函数不会修改原有序列

代码如下:

list = \[1, 2, 3, 4, 5, 6, 7, 8, 9, 10\] slice = random.sample(list, 5)  # 从list中随机获取5个元素，作为一个片断返回 print slice print list  # 原有序列并没有改变

  随机整数：

代码如下:

\>>> import random >>> random.randint(0,99) # 21

  随机选取0到100间的偶数：

代码如下:

\>>> import random >>> random.randrange(0, 101, 2) # 42

  随机浮点数：

代码如下:

\>>> import random >>> random.random() 0.85415370477785668 >>> random.uniform(1, 10) # 5.4221167969800881

  随机字符：

代码如下:

\>>> import random >>> random.choice('abcdefg&#%^\*f') # 'd'

  多个字符中选取特定数量的字符：

代码如下:

\>>> import random random.sample('abcdefghij', 3) # \['a', 'd', 'b'\]

  多个字符中选取特定数量的字符组成新字符串：

代码如下:

\>>> import random >>> import string >>> string.join( random.sample(\['a','b','c','d','e','f','g','h','i','j'\], 3) ).replace(" ","") # 'fih'

  随机选取字符串：

代码如下:

\>>> import random >>> random.choice ( \['apple', 'pear', 'peach', 'orange', 'lemon'\] ) # 'lemon'

  洗牌：  

代码如下:

\>>> import random >>> items = \[1, 2, 3, 4, 5, 6\] >>> random.shuffle(items) >>> items # \[3, 2, 5, 6, 4, 1\]