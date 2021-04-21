---
title: html  文档基本格式
tags: []
id: '553'
categories:
  - - HTML和CSS
date: 2019-02-21 18:11:15
---

下标 和 上标代码如下 `这是 <sub> 下标</sub> 和 <sup> 上标</sup>` sub下标     sup上标 **粗体** ：<strong> _斜体_：<em> 更多html字体样式[http://www.runoob.com/html/html-formatting.html](http://www.runoob.com/html/html-formatting.html) 在HTML文档中插入ID:

`<a id="tips">有用的提示部分</a>`

在HTML文档中创建一个链接到"有用的提示部分(id="tips"）"：

`<a href="#tips">访问有用的提示部分</a>`

或者，从另一个页面创建一个链接到"有用的提示部分(id="tips"）"：

`<a href="http://www.runoob.com/html/html-links.html#tips">` `访问有用的提示部分</a>`

a标签中的href可以放入mailto，可以指定一个让用户发送邮件的地址

html  head标签详细讲解[http://www.runoob.com/html/html-head.html](http://www.runoob.com/html/html-head.html)

头部引入外部css方法

<head>
<link rel\="stylesheet" type\="text/css" href\="mystyle.css"\>
</head>

也可以直接在html当中指定css样式

`<h1 style="font-family:verdana;">一个标题</h1>`

图片分区域点击

在html中，如果前面有浮动元素，后面的元素不想浮动，可用clear:both清除浮动

使用iframe来显示目标链接页面 iframe可以显示一个目标链接的页面目标链接的属性必须使用iframe的属性，如下实例: 实例 `<iframe src="demo_iframe.htm" name="iframe_a"></iframe>` `<a href="http://www.runoob.com" target="iframe_a">点击在本页打开这个链接，因为制定了target="iframe_a"</a>`

颜色：

background:rgba(255,0,0,0.5); /\* #ff0000   最后一位是透明度，0代表全透明  \*/

特殊符号在html中的转义    < > © & [http://www.runoob.com/html/html-entities.html](http://www.runoob.com/html/html-entities.html) html常用标签速查列表：[http://www.runoob.com/html/html-quicklist.html](http://www.runoob.com/html/html-quicklist.html)