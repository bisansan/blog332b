---
title: Path.resolve()   Node.js文件路径转化
tags: [nodejs,javascript]
id: '788'
categories:
  - - 计算机编程
abbrlink: '93471434'
date: 2019-08-12 11:03:27
---

```
> var path = require('path')
undefined
> path.resolve('./11')
'/home/witt/11'
> path.resolve('111')
'/home/witt/111'
> path.resolve('../1111')
'/home/1111'
> path.resolve('root','111')
'/home/witt/root/111'
> path.resolve('/root','111')
'/root/111'
> path.resolve('/root/','/111/')
'/111'
> path.resolve('a','/b','c')
'/b/c'
```

由上面可以知道，字符串是可以拼接路徑的

path.resolve可以接受多個參數來進行拼接路徑，當它沒有參數時測輸出當前路基

如果是有參數加入

./和字符前面不加符号代表和当前路径进行拼接

```
> path.resolve('./11')
'/home/witt/11'
> path.resolve('111')
'/home/witt/111'
```

只有斜杠/代表绝对路径，当有多个参数时候，有多个绝对路径，以最后一个为主，和后面的进行拼接

```
> path.resolve('/root','111')
'/root/111'
> path.resolve('/root/','/111/')
'/111'
> path.resolve('a','/b','c')
'/b/c'
```

当出现两个点加一个斜杠../当回到上一个目录

```
> path.resolve()
'/home/witt'         //输出的是当前目录
> path.resolve('../1111')
'/home/111'
```