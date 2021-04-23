---
title: css布局flex大致用法
tags: [css,flex,html,javascript]
id: '874'
categories:
  - - 计算机编程
abbrlink: 40758ff2
date: 2019-10-12 11:21:45
---

阮一峰 的基础语法详细介绍

[http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

实例介绍

[http://www.ruanyifeng.com/blog/2015/07/flex-examples.html](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

主元素被设置flex后的属性

flex-direction属性 设置主轴的方向

*   row 默认值 主轴为水平方向，从左到右
*   row-reverse 主轴为水平方向，从右到左
*   column 主轴为树直方向，从上到下
*   column-reverse 主轴为树直方向，从下到上

flex-wrap属性 设置子元素在主元素内主轴方向换行方式

*   nowarp 默认不换行，全部集中在一行，每个子元素按比例占用主元素的宽度
*   warp 自动换行，子元素放不下，自动转到下一行，第一行在首行，最后一行在底部
*   wrap-reverse 自动换行，第一行在底部，最后一行在首行

flex-flow 上面元素简写，同时设置上面两个元素，例如

```
flex-flow: row warp;
```

justify-content 设置主轴方向的子元素对其方式

*   flex-start 默认从左到右
*   flex-end 从右到左
*   center 居中
*   space-between 两端对齐，子元素之间的间距相等
*   space-around 等分对齐，子元素之间的间距相等，同时还包括左右两侧子元素到边框的距离

align-items 交叉轴对其方式

*   stretch 默认子元素等分，交叉轴的高度
*   flex-start 以交叉轴的顶部对齐
*   flex-end 以交叉轴的底部对齐
*   center 以交叉轴的中点对齐
*   baseline 以第一行文字的基线（第一行文字的底部，哪怕是文字大小不一样）

align-content 多跟轴线的对齐方式，一根轴线不起作用

*   `flex-start`：与交叉轴的起点对齐。
*   `flex-end`：与交叉轴的终点对齐。
*   `center`：与交叉轴的中点对齐。
*   `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
*   `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
*   `stretch`（默认值）：轴线占满整个交叉轴。

子元素 可以设置的属性

order 负责子元素的排序，值越小越靠前

flex-grow 默认为0不放大，设置子元素之间放大比例，也就是一个子元素在主元素中一行宽度的占用比例

假如有三个50x50子元素放在一个宽度为400的主元素盒子内，设置其中的一盒子为2，其他盒子为1，那么实际的效果是，设置为2的盒子的宽度为50+((400-150)\*(2/4))=175，其他的两个盒子就是50+((400-150)\*(1/4))=112.5

flex-shrink 定义子元素在一行项目的缩小比例，默认为1

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

flex-basis属性

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

flex: 可以一次性简写上面三个属性

```
flex: none  [ <'flex-grow'> <'flex-shrink'>?  <'flex-basis'> ]
```

align-self 可以设置单个子元素的对齐方式，会覆盖父元素设置align-items

```
align-self: auto  flex-start  flex-end  center  baseline  stretch;
```