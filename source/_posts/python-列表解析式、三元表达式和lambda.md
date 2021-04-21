---
title: python  列表解析式、三元表达式和lambda
tags: []
id: '840'
categories:
  - - Python
date: 2019-09-10 10:12:22
---

**列表解析 List Comprehensions**表达式：\[expression for iter\_val in iterable if cond\_expr\]

*   **\[expression\]**：最后执行的结果
*   **\[for iter\_val in iterable\]**：这个可以是一个多层循环
*   **\[if cond\_expr\]**：两个for间是不能有判断语句的，判断语句只能在最后；顺序不定，默认是左到右。

```
str = '332b.com'

s = [s.upper() for s in str if s.isdigit() or s.isalpha()]

print(s)


#  输出结果  ['3', '3', '2', 'B', 'C', 'O', 'M']

# s.upper() : 单词首字母大写     s.isdigit()：判断是否是数字     s.isalpha()：判断是否字母

# 执行最后的结果首字母大写，for...in循环str字符串，if如果满足条件才会得到结果
```

**三元表达式** a if b else c

*   a : 真值
*   b : 判断条件，true时执行真值，false时执行假值
*   c : 假值

```
def func(x,y):

    return x if x > y else y

print(func(1,3))

#  输出3
```

**匿名函数** lambda x,y :x\*3

前面为参数，后面是返回结果，以分号隔开，可以和三元表达式配合使用

```
# 方式一
print((lambda x,y: x*y)(2,3))

# 方式二
func = lambda x,y: x*y
print(func(2,3))
```