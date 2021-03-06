---
title: CSS学习：HTML定位流
tags: [css,html]
id: '579'
categories:
  - - 计算机编程
abbrlink: 94c798a
date: 2019-03-08 15:08:24
---

z-index定义定位流中的层级关系 注意：这个属性不能再标准流中使用 相对定位      `position: relative;` 相对定位是相对于原来的位置偏移，他有上下左右方向，x轴（左右）和y轴（上下）都只能有一个方向 注意点： 1.相对定位是不脱离标准流，它会占用标准流的空间，并且它还区分行内元素、块级元素和行内块级元素 2.给相对定位元素设置padding和margin会影响它在标准流的布局，它的padding和margin是设置相对于没有偏移前的位置 3.它的只要作用是针对于元素进行微调和结合绝对定位进行结合使用   绝对定位        `position:absolute` 绝对定位是相对于body边框的定位，绝对定位的元素是浮动元素，所以它不区分行内、块级和行内块级元素 绝对定位的参考点 可以作为绝对定位的的参考点，有以下定位流可以，绝对定位、相对定位和固定定位，静态定位不可以作为绝对定位参考点 注意点 1.如果绝对定位以body为边框，那么它的定位会以当前窗口为标准，而不是整个body窗口的真实大小 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2019/03/2019-03-08-14-17-35-的屏幕截图.png) 2.绝对元素只能以最靠近定位流为参考点，如果没有则以body为参考点 3.父元素的padding内边距不会影响绝对定位的位置   **绝对定位元素水平居中** 如何让一个`relative`中的`absolute` 水平居中 给`absolute`设置 left:50% margin-left:值为`relative` 盒子宽度的一般   固定定位                `position:fixed` 1.固定定位跟绝对元素一样，他也会和浮动元素脱落标准流 2.固定定位不会随着鼠标滚动而滚动，它的方向（left等等）都是相对于当前窗口而言 3.它还有类似的设置，背景设置background-attachment:fixed