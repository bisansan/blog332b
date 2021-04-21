---
title: python @property  动态属性和setter重新赋值
tags: []
id: '858'
categories:
  - - uncategorized
abbrlink: 1e12185b
date: 2019-09-28 17:45:02
---

直接上代码

```
class Abc(object):
    def __init__(self):
        self._value_b = 0

    def value_a(self):
        a = 128
        return a

    # 加了@property就可以将这个函数的返回值，当成属性来使用
    @property
    def value_b(self):
        b = 256
        return b

    @value_b.setter
    def value_b(self,value):
        self._value_b = value


if __name__ == '__main__':
    abc = Abc()
    print('abc.value_a:',abc.value_a())
    print('abc.value_b:',abc.value_b)
    # 重新赋值
    abc.value_b = 30
    # 重新赋值后，但是也不起作用，打印的还是原值
    print('重新赋值abc.value_b:', abc.value_b)
    # 然后使用setter，打印的值就是我们想要的了
    print('abc._value_b:', abc._value_b)
```

这里是打印结果

```
# abc.value_a: 128
# abc.value_b: 256
# 重新赋值的abc.value_b: 256
# abc._value_b: 30
```