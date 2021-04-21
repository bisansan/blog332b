---
title: C语言基础：指针函数
tags: []
id: '731'
categories:
  - - C语言
abbrlink: a721b297
date: 2019-07-31 18:01:47
---

定义指针函数，通过变量将值传入函数内，再用指针带回

1.先声明指针函数

2.创建指针函数

3.在指定区域使用它

```
#include <stdio.h>

//   先声明
void minmax(int a,int b,int *min,int *max);    

int main() {
    int a1 = 9;
    int a2 = 7;
    int min,max;
//    在这里使用指定函数
    minmax(a1,a2,&min,&max);
    printf("小的值为：%d，大的值为：%d\n",min,max);
    return 0;
}

//   在这里定义指针函数
//   它也可以放在文件声明指针函数下面
void minmax(int a,int b,int *min,int *max){
    if (a < b){
        *min = a;
        *max = b;
    } else {
        *min = b;
        *max = a;
    }
}
```

使用指针变量的，要注意定义指针变量之后，如果没有指定地址，就开始赋值，那么它就会指向一个莫名奇妙的地方，例如下面是错误的

```
//   下面是错误的
int *ab;
*ab = 3;
```