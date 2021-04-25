---
title: CSS学习：盒模型
tags: [css,html]
id: '490'
categories:
  - - 计算机编程
abbrlink: cb25ebcd
date: 2019-01-23 12:38:08
---

**边框属性** 单独给某一个方向设置边框 上：border-top 下：border-bottom 左：border-left 右：border-right 给四个方向统一设置边框：border 他们的格式为border：边框宽度 边框样式 边框颜色 边框样式：[http://www.w3school.com.cn/tiy/t.asp?f=csse\_border-style](http://www.w3school.com.cn/tiy/t.asp?f=csse_border-style)

 border-top: 2px solid blue;

  同时给四个方向设置边框 给四个方向设置不同的颜色，依次排序是上、右、下、左

border-color: red pink yellow aliceblue;

给上下，左右各设置统一样式

border-color: red pink;

border-width   设置宽度，用法同上 border-style  设置样式，用法同上 他们的取值可以是none，就代表没有属性，最大左右是覆盖自己不想要的区域   内边距：padding 内容和边框之间的距离，它的用法和上面一样，padding也有padding-width、padding-style等等，不同的是 1.使用内边距之后，内边距会改变原边框的大小 2.内边框也会有背景颜色   外边距：margin 标签与标签之间的距离，它的用法和上面一样，margin也有margin-width、margin-style等等 外边距合并现象是指外边距在垂直方向时，两个标签同时有垂直方向外边距，那么标签外边距大的会覆盖小的； http://www.w3school.com.cn/css/css\_margin\_collapsing.asp   margin注意点： 1.两个盒子是嵌套关系，里面的盒子设置了外边距，那么外面的盒子就会使用里盒子的外边距，而里面盒子的外边距不会改变，参考外边距合并 2.解决上面的方法是给外面的盒子设置边框，例如border: 5px solid #000;，就不会出现这种情况 3.在企业开发中，要控制嵌套关系首先考虑padding，再才考虑margin，margin的主要作用是用来控制兄弟关系之间的距离 margin设置水平居中方法：margin：0 auto；，垂直居中是无法使用margin实现的，它只能通过px像素控制   box-sizing   Css3推出的 box-sizing:border-box;可以将盒子放在一起，让它固定到一个圈子里面，不会出现到处跑的情况   清楚默认边距 事实上，很多标签在浏览器中都有默认边距，那么这样就不理于我们进行css定位，我可以可以通过以下方法清楚所有标签的默认边距 1.利用通配符去遍历每个标签，缺点是性能低

\* {
    padding: 0px;
    margin: 0px;
}

2.利用下面CSS样式，直接屏蔽指定标签（推荐）

body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td{
    margin:0;
    padding:0;
}

3.在html引入css样式，参考文档https://yuilibrary.com/yui/docs/cssreset/

<link rel\="stylesheet" type\="text/css" href\="http://yui.yahooapis.com/3.18.1/build/cssreset/cssreset-min.css"\>

    行高line-height line-height为一行的行高，下面是设置示例

line-height: 20px;

1.在企业开发中，我们要保证一行文字正好在一个文本框中居中，最常见的就是直接将行高和盒子的高度设置成一样 2.如果是两行或者多行的话，我们可以这样设置，通过padding内边距来控制，然后用box-sizing:border-box;把文字固定到一个文本框中 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/QQ截图20190124152329.png)

<head>
    <meta charset="UTF-8">
    <style type="text/css">
        body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td{
            margin:0;
            padding:0;
        }
        div {
            width: 80px;
            height: 80px;
            border: 1px solid #000;
            line-height: 20px;
            box-sizing:border-box;
            padding-bottom: 20px;
            padding-top: 20px;
        }
    </style>
    <title>首页</title>
</head>
<body>
<div>
    <p>我是文字1</p>
    <p>我是文字2</p>
</div>

  文字和字号 1.在企业开发中，盒子储存文字的形式，一般是以左边的内边距为准，因为会有误差，这个误差是由于换行导致的 2.文字的内边距不是文字直接到边框的距离，而是内边距+行高