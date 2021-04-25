---
title: 浮动流排版：清楚默认边距和清除浮动的5种方式
tags: [css,html]
id: '500'
categories:
  - - 计算机编程
abbrlink: 7146a28f
date: 2019-01-24 17:30:13
---

浮动流 是一种半脱离标准的排版方式 注意点： 1.浮动流中没有居中对齐，也没有center这个取值 2.浮动流中margin: 0 auto;是不能使用的   特点： 1.浮动流是不区分块级元素、行内元素和行内块级元素，并且他们都会可以设置长宽高   **浮动元素脱标和它带来的影响** 什么是浮动元素脱标？ 一个元素浮动之后，它就像是从标准流中删除了一样，这个就称之为浮动元素的脱标   它会有什么影响？ 当一个元素浮动后，后跟紧跟后面的一个元素如果没有浮动，那么这个元素就会盖住紧跟着的那个没有浮动的元素   浮动元素的贴靠现象

什么是浮动元素贴靠现象?
1.如果父元素的宽度能够显示所有浮动元素, 那么浮动的元素会并排显示
2.如果父元素的宽度不能显示所有浮动元素, 那么会从最后一个元开始往前贴靠
3.如果贴靠了前面所有浮动元素之后都不能显示, 最终会贴靠到父元素的边框底下

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/1.png)   浮动元素字围现象 浮动的元素不会盖住没有浮动元素中的文字，没有浮动元素中的文字会给浮动的元素让位置，字围效果可以用来做图文混排 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/2.png) **清除浮动方式** 例如下面代码，会向下面这样显示，因为它的p标签是浮动，div已经被清除了margin和padding，所以没有占面积，如果我们要清除浮动，下面就介绍清除方式 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/20190125154627.png)

 <style type="text/css">
           body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td {
            margin:0; padding:0;
        }
        .a1 {
            background-color: #00F7DE;

        }
        .a2 {
            background-color: #0000FF;
            /\* clear: left; \*/
        }
        .a3 {
            background-color: #00F7DE;

        }
        p {
            background-color: #00FF00;
            float: left;
        }
    </style>
</head>
<body>
<div class="a1">
    <p>aaaaa</p>
</div>
<div class="a2">
    <p>
        bbbbbbb
    </p>
</div>
<div class="a3">
    <p>
        cccccc
    </p>
</div>

1.给div设置高度，例如给a1设置100的高度，后面的p标签就不会找它，但是因为我们在开发能不设置高度，就不要高度（这个方法不常用） ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/20190125154706.png) 2.给p标签添加clear: left;，就会向下面这样显示，clear有both(两边都不要浮动),left（左不要浮动）,right（右边不要浮动） ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/20190125154930.png) 3.内墙法和外墙法 他们的不同之处和相同点 他们两个共同点都是隔开两个元素，都需要如下的一个div代码，都可以让第二个盒子设置margin-top属性

<div style="clear:both"></div>

不同点 1.内墙法要在内部元素设置<div style="clear:both"></div>，外墙法则是在两个块级元素之间设置 2.内墙法可以让第一个元素设置margin-bottom，而外墙法不可以 3.内墙法可以撑起它设置的那个盒子的高度，而外墙法不可以   4.伪元素选择器

<style type="text/css">
    div::after {
        content: "洗刷回溯爱之伤情"; /\* 只能添加字符串，不能添加html标签\*/
        width: 50px;
        height: 0px;
        background-color: #00FF00;
        display: block;    /\*作为块级元素\*/
        visibility: hidden;   /\* 设置是否隐藏\*/
    }
</style>
<div>我是文字</div>

div::after 在div标签后面添加元素，div::before  在div标签前面添加元素

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>69-清除浮动方式四</title>
    <style>
        \*{
            margin: 0;
            padding: 0;
        }
        .box1{
            background-color: red;
            /\*margin-bottom: 10px;\*/
        }
        .box2{
            background-color: green;
            /\*margin-top: 10px;\*/
        }
        .box1 p{
            width: 100px;
            background-color: blue;
        }
        .box2 p{
            width: 100px;
            background-color: yellow;
        }
        p{
            float: left;
        }
        .box1::after{
            /\*设置添加的子元素的内容为空\*/
            content: "";
            /\*设置添加的子元素为块级元素\*/
            display: block;
            /\*设置添加的子元素的高度为0\*/
            height: 0;
            /\*设置添加的子元素看不见\*/
            visibility: hidden;
            /\*给添加的子元素设置clear: both;\*/
            clear: both;
        }
        .box1{
            /\*兼容IE6\*/
            \*zoom:1;
        }
    </style>
</head>
<body>
<!--
1.清除浮动的第四种方式
利用伪元素选择器清除浮动
本质上就是内墙法, 只不过是直接通过CSS代码添加了内墙, 其它特性和内墙法都一样

注意点:
IE6中不支持这种方式, 为了兼容IE6必须给前面的盒子添加\*zoom:1;属性
-->
<div class="box1">
    <p>我是文字1</p>
    <p>我是文字1</p>
    <p>我是文字1</p>
</div>

<div class="box2">
    <p>我是文字2</p>
    <p>我是文字2</p>
    <p>我是文字2</p>
</div>
</body>
</html>

  5。就是直接在css添加overflow: hidden;，这个属性还可以 1.这个css属性可以清除浮动 2.可以将超出范围的内容裁剪 3.可以让里面的盒子设置margin-top，外面的盒子不被顶下来 解决IE6兼容：再添加\*zoom:1;