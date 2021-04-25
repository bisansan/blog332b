---
title: CSS学习：背景和精灵图
tags: [css,html]
id: '482'
categories:
  - - 计算机编程
abbrlink: 7413711c
date: 2019-01-23 10:12:52
---

background意思为背景，在css中起来设置背景的作用 background-color 设置背景颜色

background-color: fuchsia;

  background-image 设置背景图片 如果图片比设定的区域小，那么它就会以平铺和填充的形式，填满整个的区域，设置图片会向服务器发送两次请求，第一下载超文本，第二次才会下载图片

background-image: url(/img/photo.png);

  background-repeat 控制平铺 它需要和background-image一起使用，作用是控制平铺和填充，它有四个属性repeat（按默认方式填充），repeat-x（只填充X轴），repeat-y（只填充Y轴），no-repeat（不填充）

.b123 {
    background-image: url(/img/photo.png);
    background-repeat: repeat;
}

  background-position 控制定位 控制图片no-repeat（不填充）的位置，如下图默认是左上角 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/01/20190122162855.png) background-position第一个为水平方向，第二为树直方向 x轴三个方向的关键词：left center right y轴三个方向的关键词：top center bottom 除了用关键词以外，还可以用像素，第一个水平向右偏移多少，第二个是向下偏移多少，写法background-position: 100px 120px; 像素是可以接受负数的，具体使用请百度，当背景颜色和图片同时存在时，图片会覆盖颜色

.b123 {
    background-image: url(/img/photo.png);
    background-repeat: no-repeat;
    background-position: left top;
}

background的简写方式：background：背景颜色  背景图片 平铺方式  关联方式  定位方式

background: red url("img/photo.png") no-repeat scroll left top;

background-attachment关联方式 控制图片是否随着滚动条的滚动而滚动 scroll（默认）：随着滚动条的滚动而滚动 fixed：会跟随当前窗口，不会随着滚动条的滚动而滚动

background-attachment: scroll;

  css精灵图 定义一个图片中的某个按钮，先规定div的大小，再通过background-position将图片偏移到指定区域

<head>
    <meta charset="utf-8">
    <title>首页</title>
    <style type="text/css">
        div {
            height: 52px;
            width: 180px;

        }
        .b123 {
            background: red url("20190123094711.png") no-repeat ;
            background-position: -130px -92px;
            background-attachment: scroll;
        }
    </style>
</head>
<body>
<div class="b123"></div>
</body>