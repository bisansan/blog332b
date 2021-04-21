---
title: python 类对象私有属性
tags: []
id: '902'
categories:
  - - uncategorized
abbrlink: 4eac8846
---

\_\_**doc\_\_** 打印类描述信息

```
class Abc(object):
    '你好,我好,大家好!'
    a = 111

print(Abc.__doc__)

# 打印'你好,我好,大家好!'
```

\_\_**module\_\_** ,\_\_name\_\_, \_\_del\_\_

\_\_**module\_\_** 打印类所在的模块

\_\_class\_\_ 打印类型,如果是class().\_\_class\_\_ 则会打印模块+类名

\_\_del\_\_ 在执行class()完毕后,执行这个