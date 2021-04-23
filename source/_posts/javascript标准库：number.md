---
title: javascript标准库：Number
tags: [javascript]
id: '742'
categories:
  - - 计算机编程
abbrlink: cc46bdda
date: 2019-08-11 18:23:40
---

Number.EPSILON 表示1和大于1且最靠近1的那个浮点数之间的差值

Number.MAX\_SAFE\_INTEGER 为最大安全整数，2的53次方减1， 9007199254740991

Number.MAX\_VALUE MAX\_VALUE 属性值接近于 1.79E+308。大于 MAX\_VALUE 的值代表 "Infinity"无穷大

Number.MIN\_SAFE\_INTEGER Number.MIN\_SAFE\_INTEGER 代表负的(2的53次方减1) -9007199254740991

Number.MIN\_VALUE MIN\_VALUE 的值约为 5e-324。小于 MIN\_VALUE ("underflow values") 的值将会转换为 0。

Number.NEGATIVE\_INFINITY 负无穷大

Number.POSITIVE\_INFINITY 正无穷大

Number.NaN 不是数字，不能表示的数字或不是有效数字

Number.isFinite(x) 方法用来检测传入的参数是否是一个有穷数，我理解是数字为true，非数字为false

Number.isInteger(x) 方法用来判断给定的参数是否为整数。

Number.isNaN(x) 方法确定传递的值是否为 NaN和其类型是 Number

Number.isSafeInteger(x) 方法用来判断传入的参数值是否是一个“安全整数，安全整数范围为 -(253 - 1)到 253 - 1 之间的整数

Number.parseFloatx() 将一个字符串转换成浮点数

Number.parseInt() 将一个字符串转换成整数

num.toExponential(x) 方法以指数表示法返回该数值字符串表示形式，我的理解是用科学计数法表示一个值，然后保留x位小数

Number.toFixed() 方法使用定点表示法来格式化一个数值，我的理解是格式化一个数字后保留小数点后多少位

Number.toPrecision() 方法以指定的精度返回该数值对象的字符串表示，我的理解：这个跟上面做对比，这个不能格式化数字

Num.toString(x) 把数字转换成字符串，X位进制单位，输出的进制单位可以在2-22之间

Number.valueOf() 方法返回一个被 Number 对象包装的原始值。

```
var numObj = new Number(10);
console.log(typeof numObj); // object

var num = numObj.valueOf();
console.log(num);           // 10
console.log(typeof num);    // number
```