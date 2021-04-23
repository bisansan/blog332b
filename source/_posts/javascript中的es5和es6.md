---
title: javascript中的ES5和ES6
tags: [javascript,es6]
id: '653'
categories:
  - - 计算机编程
abbrlink: c739c9e4
date: 2019-06-03 15:15:50
---

ES6 1.块级作用域 let     变量 const    常量   for (let a = 1;a<8;a++){ let a = 12 }   let不能被覆盖，上面for循环两个a是在两个单独和独立的块级作用域里面，他们是不能互相沟通 const 不能被修改，但是如果const定义的是个数组，是可以改变数组里面的值，这个是对象的特性，但是不能改变const赋值的类型 如果你想定义一个不能修改的对象，es6新增了一个OBject.freeze(\['1','2'\])   es6中的暂时性死区 ｛ console.log(a) let = a; ｝ 当你还没定义变量A，却在定义之前使用了这个变量，定义这个变量前面的区域就称之为暂时性死区   2.解构赋值 let \[a,b,p=3\] = \[1,2\]; 列表赋值三个变量，也可以直接设置默认值

let {e,c,d} = {e:4,c:5,d:6}

对象也可以这样赋值

let f;

({f} = {f:7});

如果先声明变量，再进行赋值，外面包裹一层小括号，可以避免直接使用大括号当成块级作用域

3.字符串模版

var a = '小明';

var str = \`亲爱的${a}，你好!\`

console.log(str);

注意变量str用的是反引号，不是普通的单双冒号

str.includes(‘a’)   返回所查找字符的位置的数字

str.indexOf(‘a’)     返回是否包含该字符的true或false