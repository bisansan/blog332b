---
title: javascript 学习：Array
tags: [javascript]
id: '730'
categories:
  - - 计算机编程
abbrlink: 578e9f64
date: 2019-08-01 14:31:54
---

属性

Array.length 给出数组的总数

Array.prototype 可以自己定义子属性

```
//   返回数组的第一个元素
    let list = [1,2,3,4];
    if(!Array.prototype.first) {
        Array.prototype.first = function () {
            return this[0];
        }
    }
    alert(list.first())
```

方法

Array.from(arrayLike\[, mapFn\[, thisArg\]\])

arrayLike  
想要转换成数组的伪数组对象或可迭代对象。  
mapFn (可选参数)  
如果指定了该参数，新数组中的每个元素会执行该回调函数。  
thisArg (可选参数)  
可选参数，执行回调函数 mapFn 时 this 对象。

```
console.log(Array.from('foo'));             // > Array ["f", "o", "o"]
```

```
console.log(Array.from([1, 2, 3, 4], x => x + x));     // > Array [2, 4, 6, 8]
```

Array.isArray(obj) 检测数组是否是数组，正确返回true，错误返回false

Array.of(element0\[, element1\[, …\[, elementN\]\]\]) 可以将多个变量一起转换成一个数组

```
//Array.of和Array类似，但是他们在遇到整数时，是有区别的

Array.of(7);           // > [7] 
Array.of(1, 2, 3);     // > [1, 2, 3]

Array(7);              // > [ , , , , , , ]
Array(1, 2, 3);        // > [1, 2, 3]
```

list1.concat(list2) 将两个数组连接组成一个数组

```
let list1 = [1,2,3,4];
let list2 = [5,6,7];
alert(Array.from(list1.concat(list2)))

// > [1,2,3,4,5,6,7]
```

arr.copyWithin(target\[, start\[, end\]\]) 对指定位进行浅复制，并放到指定位置

```
var array1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l'];

console.log(array1.copyWithin(5));
// 复制前面的(0,4)放在5的位置
// > Array ["a", "b", "c", "d", "e", "a", "b", "c", "d", "e", "f", "g"]

console.log(array1.copyWithin(1,10));
// 复制(10,最后一位)放在1的位置
// > Array ["a", "k", "l", "d", "e", "f", "g", "h", "i", "j", "k", "l"]

console.log(array1.copyWithin(1,2,5))
// 复制(2,5)放到1的位置
// > Array ['a', 'c', 'd', 'e', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l']
```

arr.entries() 生成一个数组的迭代器，可以用arr.entries().next()依次执行，来获取每个值的序列号

```
//  用for...of...来循环迭代器
var array1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l'];
let p = array1.entries();

// 也可以用p.next()来依次执行，获取每个值和序号
for (let i of p) {
    console.log(i)
}
```

arr.fill(value\[, start\[, end\]\]) 用一个指定的值来填充指定的范围的每个元素

value：值 start：起始值，默认是0 end：结束值，默认是结尾

```
var array1 = [1, 2, 3, 4];

// 用0来填充(2,4)中的所有值
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]

// 用5来填充(1,最后一位)的所有值
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

// 用6填充里面的所有值
console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]
```

arr.every(callback\[, thisArg\]) 用回调函数来得到每个值的true和false，数组内只要有一个值返回false，那么它就不会向下执行了，整个函数结果就返回false，如果每个值返回的都是true，那么它返回就是true

**注意：若收到一个空数组，此方法在一切情况下都会返回 true。**

```
   //element当前值，index序号，array当前执行的数组
    function iss(element,index,array) {
        alert(array);
        return true
    }

    var array1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l'];
    console.log(array1.every(iss));
```

arr.filter(callback\[, thisArg\]) 过滤不符合的值，组成一个新的数组

```
    function iss(element,index,array) {
        if (index > 3) {
            return true
        } else {
            return false
        }
    }
    var array1 = [1,2,3,4,5,6,7];
    console.log(array1.filter(iss));
```

arr.find(callback\[, thisArg\]) 返回符合条件的第一个值，否则返回 undefined

arr.findIndex(callback\[, thisArg\]) 返回符合条件的第一个值的索引

arr.flat(depth) 深度递归数组里面的每个数组，并把所有遍历到的结果组成一个新数组

depth 为递归深度，默认是1，如果值设置Infinity那就是无限制网下递归

```
var arr1 = [1, 2, [3, 4]];
arr1.flat(); 
// [1, 2, 3, 4]

var arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

var arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]

//使用 Infinity 作为深度，展开任意深度的嵌套数组
arr3.flat(Infinity); 
// [1, 2, 3, 4, 5, 6]
```

arr.flatMap(depth) 遍历数组内的每个元素，并返回新值

function callback(currentValue\[, index\[, array\]\]  
可以生成一个新数组中的元素的函数，可以传入三个参数：

currentValue  
当前正在数组中处理的元素  
index可选  
可选的。数组中正在处理的当前元素的索引。  
array可选  
可选的。被调用的 map 数组  
thisArg可选  
可选的。执行 callback 函数时 使用的this 值。

```
//map和flatMap是有细微的区别的
var arr1 = [1, 2, 3, 4];

arr1.map(x => [x * 2]); 
// [[2], [4], [6], [8]]

arr1.flatMap(x => [x * 2]);
// [2, 4, 6, 8]

// 只会将 flatMap 中的函数返回的数组 “压平” 一层
arr1.flatMap(x => [[x * 2]]);
// [[2], [4], [6], [8]]

let arr = ["今天天气不错", "", "早上好"]

arr.map(s => s.split(""))
// [["今", "天", "天", "气", "不", "错"],[""],["早", "上", "好"]]

arr.flatMap(s => s.split(''));
// ["今", "天", "天", "气", "不", "错", "", "早", "上", "好"]
```

arr.forEach(callback\[, thisArg\]); 为数组内的每个元素执行一次函数，它不会改变数组内的值

```
    function iss(element,index,array) {
        console.log(element+1)
    }
    var array1 = [1,2,3,4,5,6,7];
    array1.forEach(iss);
// > 1
// > 2
// > 3
............
```

arr.includes(valueToFind\[, fromIndex\]) 检测一个数组是否包含指定值

```
var pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true
```

arr.indexOf(searchElement\[, fromIndex = 0\]) 查找指定元素，返回指定元素的索引，如果没找到返回-1

```
var beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4
```

Array.join() 将数组内的元素拼接成字符串

```
var elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```

arr.keys() 将数组的索引生成一个迭代器

```
var array1 = ['a', 'b', 'c'];
var iterator = array1.keys(); 
  
for (let key of iterator) {
  console.log(key); // expected output: 0 1 2
}
// > 0
// > 1
> 2
```

arr.lastIndexOf() 从数组的最后一个开始查找，查找成功返回索引，失败测返回-1

```
var animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

console.log(animals.lastIndexOf('Dodo'));
// 输出: 3

console.log(animals.lastIndexOf('Tiger'));
// 输出: 1
```

arr.map() 为每个值提供一个函数并返回一个新数组，它有回调function callback(currentValue\[, index\[, array\]\])

```
var array1 = [1, 4, 9, 16];

// 创建map
const map1 = array1.map(x => x * 2);

console.log(map1);
// 输出新数组 [2, 8, 18, 32]
```

arr.pop() 删除最后一个值并返回该值

arr.push() 在末尾追加新元素，可以添加一个或者多个

```
var animals = ['pigs', 'goats', 'sheep'];

console.log(animals.push('cows'));
// 添加之后变成: 4个

console.log(animals);
// 输出: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens', 'good');

console.log(animals);
// 输出: Array ["pigs", "goats", "sheep", "cows", "chickens", "good"]
```

arr.reduce() 从左到右为每一个元素执行 一次reduce提供的函数，返回最后一次执行的累计结果

arr.reduceRight() 从右到左，方法同上

arr.reduce(callback(accumulator, currentValue\[, index\[, array\]\])\[, initialValue\])

callback  
执行数组中每个值的函数，包含四个参数：  
accumulator  
累计器累计回调的返回值; 它是上一次调用回调时返回的累积值，或initialValue（见于下方）。

currentValue  
数组中正在处理的元素。  
currentIndex可选  
数组中正在处理的当前元素的索引。 如果提供了initialValue，则起始索引号为0，否则为1。  
array可选  
调用reduce()的数组  
initialValue可选  
作为第一次调用 callback函数时的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。

```
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

arr.reverse() 数组反转，颠倒数组的顺序

```
var array1 = ['one', 'two', 'three'];
console.log('array1: ', array1);
// expected output: Array ['one', 'two', 'three']

var reversed = array1.reverse(); 
console.log('reversed: ', reversed);
// expected output: Array ['three', 'two', 'one']
```

arr.shift() 删除数组的第一个值并返回

arr.slice() 截取数组的一部分并返回一个新数组

```
var animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]
```

arr.some() 为每一个值执行一次函数，只要有一个值返回true，那么它就返回true

arr.some(callback(element\[, index\[, array\]\])\[, thisArg\])

```
var array = [1, 2, 3, 4, 5];

var even = function(element) {
  // checks whether an element is even
  return element % 2 === 0;
};

console.log(array.some(even));
// expected output: true
```

arr.splice() 在指定位中删除或修改后，再新增元素，这个会改变原数组

```
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'May']
```

arr.toString() 将数组转换成字符串

```
var array1 = [1, 2, 'a', '1a'];

console.log(array1.toString());
// expected output: "1,2,a,1a"
```

arr.unshift() 在开头添加一个或者多个值，并返回数组的长度

```
var array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```

arr.values() 返回包含数组所有值的一个迭代器

```
const array1 = ['a', 'b', 'c'];
const iterator = array1.values();

for (const value of iterator) {
  console.log(value); // expected output: "a" "b" "c"
}
```