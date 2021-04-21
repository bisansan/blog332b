---
title: C语言：指针变量的使用
tags: []
id: '748'
categories:
  - - C语言
abbrlink: a1291b2d
date: 2019-08-09 17:32:05
---

初始化一个指针变量

```
int *point ;
```

将一个指针变量指向一个变量

```
int number = 32;
int *point;
point = &munber;
```

还有一种更简介的写法

```
int number = 32;
int *point  = &munber;
```

指针变量的输出

```
int number = 32;
int *point  = &munber;
printf("%d", *point);
```

下面的写法是错误的，不允许这样写，千万不要将指针变量指向一个值

```
int *point = 12;
```