---
title: CSS3学习：Transform 2D转换
tags: []
id: '595'
categories:
  - - HTML和CSS
date: 2019-03-27 10:29:55
---

  顺时针旋转45度 transform: rotate(45deg);   控制x,y轴的偏移 transform: translate(100px,50px);   控制x,y轴的缩放 transform: scale(2,2);   需要进行多个属性的转换请用空格隔开，2D转换会改变原来的坐标系，例如你想先旋转后平移，结果并不是水平平移[2D转换.html](https://post.332b.com/wp-content/uploads/2019/03/2D转换.html)   形变中心点 可以改变transform: rotate旋转的中心点，旋转一般是以自己的中心点作为旋转点 transform-origin:20px 0;  /\*（X和Y轴）\*/ 它可以用px、百分比和center,left等为单位   元素距离视图的距离 perspective: 500px; 注意：这个属性必须添加到旋转元素的父级元素   设置以X轴来旋转，默认是以Z轴 transform:rotateX(-180deg);   [图片旋转.html](https://post.332b.com/wp-content/uploads/2019/03/图片倾斜.html)