---
title: HTML：表格
tags: [css,html]
id: '295'
categories:
  - - 计算机编程
abbrlink: 9f83832e
date: 2018-11-23 15:05:59
---

<caption></caption>是列表的标题（可选），<table></table>表格标签，<tr></tr>代表表格中的一行，<td></td>代表表格中一个单元格，表格默认是没有边框的，可以通过border="1"这个属性来设置标签，<th>可以作为表格列的标题；

<table border="1">
    <caption>
        <h2>我是列表标题</h2>
    </caption>
   <tr>
        <th>当前列标题1</th>
        <th>当前列标题2</th>
    </tr>
    <tr>
        <td>小苹果</td>
        <td>小苹果</td>
    </tr>
    <tr>
        <td>小苹果</td>
        <td>小苹果</td>
    </tr>
</table>

### 1.表格的高度和宽度使用方法

高度和宽度只能用在table和td标签，在table中width和height可以整个表格的高度，在td中width和height可以改变当前单元格的高度，不会影响整个单元格的高度

### 2.水平对齐和垂直对齐

水平对齐可以给table、td和tr标签使用，align属性的left、right和center控制水平方向左、右和居中   垂直对齐只能给table和td标签使用，vlign属性的top、middle和bottom可以控制垂直方向的顶部、中间和底部

### 3.外边距和内边距

内边距和外边距只能给table使用，内边距是指单元格内的文字距离单元格的距离，cellpadding属性可以控制距离，默认是0px，外边距是表格中的单元格和单元格之间的距离，默认是2px的距离，cellspacing属性可以控制距离

### 细线表格

细线表格的实现，通过将整个背景颜色设置为黑色，单元格的背景颜色设置为白色，内边距设置为1，代码如下

<table BGCOLOR="black" cellspacing-="1">
    <tr BGCOLOR="#f0f8ff">
        <td>111</td>
        <td>222</td>
    </tr>
    <tr bgcolor="#f0f8ff">
        <td>333</td>
        <td>444</td>
    </tr>
</table>

一个超有趣的图案

<table bgcolor="black" width="500px" height="300px" align="center">
    <tr bgcolor="white">
        <td colspan="2"></td>
        <td rowspan="2"></td>
    </tr>
    <tr bgcolor="white">
        <td rowspan="2"></td>
        <td bgcolor="black"></td>
    </tr>
    <tr bgcolor="white">
        <td colspan="2"></td>
    </tr>
</table>