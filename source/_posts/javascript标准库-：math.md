---
title: javascript标准库 ：Math
tags: [javascript]
id: '738'
categories:
  - - 计算机编程
abbrlink: 5d24a3b
date: 2019-08-05 09:55:32
---

Math.abs(a) 算绝对值，数字算出正数，null还是0，非数字和null返回Nan，即无法计算的数字

Math.cbrt(a) 算出一个值的立方根

Math.ceil(a) 向上取整（上为正数，中间是0，下为负数）

```
Math.ceil(47.8)  // > 48
Math.ceil(47.1)  // > 48
Math.ceil(-47.1)  // > -46
```

Math.floor(a) 向下取整

```
Math.ceil(47.8)  // > 47
Math.ceil(47.1)  // > 47
Math.ceil(-47.1)  // > -48
```

Math.max(a,b,c...) 在多个值里面取出最大的

Math.min(a,b,c...) 找出多个值里面最小的

```
高级用法，算一个数组的最大或者最小值参考
https://www.cnblogs.com/moqiutao/p/7371988.html
```

Math.pow(x,y) 算出一个数字的多少次幂

```
Math.pow(3,2)   // > 9   3的2次方（也就是平方）
Math.pow(3,3)   // > 27  3的3次方（也就是立方）
```

Math.round(x) 对一个值进行四舍五入

Math.random() 返回一个0-1之间的随机浮点数

Math.sign(x) 函数返回一个数字的符号, 指示数字是正数，负数还是零。

```
Math.sign(3);     //  1
Math.sign(-3);    // -1
Math.sign("-3");  // -1
Math.sign(0);     //  0
Math.sign(-0);    // -0
Math.sign(NaN);   // NaN
Math.sign("foo"); // NaN
Math.sign();      // NaN
```

Math.sqrt(x) 返回一个数字的平方根

Math.trunc() 方法会将数字的小数部分去掉，只保留整数部分。