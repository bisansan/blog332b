---
title: CSS学习：a标签伪类选择器和过渡模块
tags: []
id: '591'
categories:
  - - HTML和CSS
abbrlink: '67200049'
date: 2019-03-25 17:51:13
---

a伪类选择器的必须放在标签后面，他们必须按照link>visited>active>hover的循序来排序，否则无效，它也可以单个或者多个，但必须遵循默认排序规则 :link a:link 选择所有未被访问的链接。 :visited a:visited 选择所有已被访问的链接。 :active a:active 选择活动链接。 :hover a:hover 选择鼠标指针位于其上的链接。   transition  过渡属性 连写方式

transition: property duration timing-function delay;

property：CSS属性    duration：设置过渡时间    timing-function：过渡速度    delay：设置从多少秒开始 如果多个transition的过渡时间一样，可以设置为transition:all 0s 如果存在多个属性使用逗号和空格隔开，分别设置就可以了

         <style type="text/css">
.d1 {
width: 100px;
height: 100px;
background: red;
transition-property: width, height, background;
transition-duration: 3s, 3s, 3s;
}
.d1:hover {
width: 300px;
height: 300px;
background: blue;
}
</style>