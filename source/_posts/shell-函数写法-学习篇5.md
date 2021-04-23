---
title: shell 函数写法 学习篇(5)
tags: [shell,linux]
id: '955'
categories:
  - - 系统运维
abbrlink: 8a123831
date: 2020-05-14 18:28:15
---

1.普通函数使用

```
# shell函数示例

# 定义函数
func1 () {
    echo "这个是函数1"
}
# 执行函数
func1
```

2.函数返回值

```
# 返回和获取函数值
function func2 () {
    number1=1
    number2=2
    number3=3
    return $(($number1+$number2+$number3))
}
func2
echo "fucn2函数之和为：$?"
```

3.函数使用参数

```
# 设置和获取函数参数
func3 () {
    echo "输出第一个函数参数：$1"
    echo "输出第二个函数参数：$2"
    echo "输出第三个函数参数：$3"
    echo "总共有函数参数个数：$#"
    echo "字符串输出所有参数：$*"
    echo "输出一个没有的参数：$9"
}

func3 1 2 3 4
```

4.一些注意事项

![](https://post.332b.com/wp-content/uploads/2020/05/screenshot-www.runoob.com-2020.05.14-18_23_17.png)