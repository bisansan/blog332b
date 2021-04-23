---
title: javascript 标准库：Object
tags: [javascript]
id: '743'
categories:
  - - 计算机编程
abbrlink: ac170978
date: 2019-08-05 18:06:27
---

Object.assign(target, source) 将两个对象禁止复制返回一个新合成的对象，注意这个两个对象 target和source如果有相同的key，那么 source 将会覆盖 target 里面的值

Object.defineProperties(obj, props) 方法直接在一个对象上定义新的属性或修改现有属性，并返回该对象。obj为一个对象，props为向里面添加key和value

Object.entries() 将对象转变一个可遍历的对象

```
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);     //就是转换成这种形式
```

Object.fromEntries() 方法把键值对列表转换为一个对象

```
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```

Object.freeze() 冻结一个对象，使得你无法修改添加和删除

Object.getPrototypeOf(object) 返回对象的原型对象

Object.is(value1, value2) 判断两个值是否相等

Object.isExtensible() 方法判断一个对象是否是可扩展的（是否可以在它上面添加新的属性）

Object.isFrozen() 查看一个对象是否被冻结

Object.isSealed(obj) 查看一个对象是否被密封

Object.keys(Obj) 返回一个对象所有的key值的列表

Object.preventExtensions(obj) 方法让一个对象变的不可扩展，也就是永远不能再添加新的属性。

obj.hasOwnProperty(prop) 检查对象是否包含某个值

obj.propertyIsEnumerable(prop) 查看指定值是否可以枚举（是否可以遍历）

object.toString() 方法返回一个表示该对象的字符串

Object.seal() 方法封闭一个对象，阻止添加新属性并将所有现有属性标记为不可配置。当前属性的值只要可写就可以改变。

Object.values(obj) 将他的值变成一个可以枚举的数组（可遍历的数组）