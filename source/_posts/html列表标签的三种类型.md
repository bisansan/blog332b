---
title: 'HTML:列表标签的三种类型'
tags: []
id: '300'
categories:
  - - HTML和CSS
date: 2018-11-21 10:26:46
---

列表的三种类型

1.  无序列表     unorder list
2.  有序列表    order list
3.  定义列表   definition list

无序列表 下面是无序列表的一个简单示例，他的作用不是为了给文字添加小圆点，html是给文本定义，css才是样式 WebStom 生成ul标签语法：ul>li\*3    生成一对ul标签和3对li标签

<ul>
    <li>列表文字1</li>
    <li>列表文字2</li>
</ul>

有序列表 它可以用来做排行，默认是以1、2、3数字排名，它自带一个属性type可以更改显示的类型

<ol>
    <li>我是第一行</li>
    <li>我是第二行</li>
</ol>

定义列表 它是由有dt和dd作为一对，一对里面dt是必须有的，dd可以没有，也可以有多个，他一般可以拿来做页脚或者其他的功能

<dl>
    <dt>我是标题</dt>
    <dd>我是内容描述</dd>
    <dt>我是标题1</dt>
    <dd>我是内容描述1</dd>
    <dd>我是内容描述2</dd>
</dl>