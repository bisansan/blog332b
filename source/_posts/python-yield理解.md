---
title: python yield理解
tags: [python]
id: '855'
categories:
  - - 计算机编程
abbrlink: 4635b714
date: 2019-09-28 12:30:09
---

先看实例

```

def foo():
    print("starting...")
    while True:
        res = yield 4
        print("res:",res)
# 迭代器
g = foo()


# 执行第一次，yield相当于return，所以就返回 4
print(next(g))


# 第二次执行，就从res = 的开始执行，yield已经将前面的值return出去了，所以就成了None
# yield 前面加‘=’，相当于可以产出该值，还可以接受过调试者传过来的值比如下面
print(next(g))

# 向生成器传值
g.send('11111111111')
```

再看打印结果

```
# 最终答应结果为
# starting...
# 4
# res: None
# 4
# res: 11111111111
```

函数内如果有yield，就代表这个函数是迭代器

注意：迭代器如果没有可以迭代的对象，执行next()就会报错