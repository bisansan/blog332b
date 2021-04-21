---
title: Javascript对象：Data和map
tags: []
id: '736'
categories:
  - - JavaScript
date: 2019-08-01 17:45:14
---

Date() 返回当前时间，也可以用来转换时间搓

```
var d=new Date();
 console.log(d)
// > Thu Aug 01 2019 15:18:46 GMT+0800 (中国标准时间)

console.log(new Date(1517446861000))

// > Thu Feb 01 2018 09:01:01 GMT+0800 (中国标准时间)
```

Date.UTC()

year  
1900 年后的某一年份。  
month  
0 到 11 之间的一个整数，表示月份。  
date  
1 到 31 之间的一个整数，表示某月当中的第几天。  
hrs  
0 到 23 之间的一个整数，表示小时。  
min  
0 到 59 之间的一个整数，表示分钟。  
sec  
0 到 59 之间的一个整数，表示秒。  
ms  
0 到 999 之间的一个整数，表示毫秒。

```
console.log(new Date(Date.UTC(2018,1,1,1,1,1,1)))

// > Thu Feb 01 2018 09:01:01 GMT+0800 (中国标准时间)
```

Date.now() 返回当前时间的UTC时间戳，注意这个时间戳，是没有时区的

```
console.log(Date.now());
// > 1564644033035
```

Date.parse() 将一个指定的时间转换成时间搓

```
var unixTimeZero = Date.parse('Thu Feb 01 2018 09:01:01 GMT+0800 (中国标准时间)');
console.log(unixTimeZero);

```

Map.size() 统计map中的所有所有键值数量

```
var map1 = new Map();

map1.set('a', 'alpha');
map1.set('b', 'beta');
map1.set('g', 'gamma');

console.log(map1.size);
// expected output: 3
```

Map.clear() 清除所有键值

Map.delete(key) 删除指定Key，如果不存在就返回false，存在就返回true

Map.entries() 将指定的map对象转换成一个迭代器

Map.forEach() 为每个值执行一次函数

myMap.forEach(callback\[, thisArg\])

callback 函数有三个参数:

value - 元素的值  
key - 元素的键  
Map - 当前正在被遍历的对象

Map.get(key) 通过键来获取值，如果找不到就是undefined

Map.has(key) 检测是否包含key，返回true或false

Map.keys() 生成一个包含所有keys值的迭代器

Map.set(key, value) 为map对象新建一个键和值

Map.values() 返回一个包含所有值的迭代器