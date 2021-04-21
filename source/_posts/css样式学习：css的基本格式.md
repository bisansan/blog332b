---
title: CSS样式学习：CSS的基本格式和选择器
tags: []
id: '422'
categories:
  - - HTML和CSS
abbrlink: fa1535a
date: 2018-12-27 21:15:22
---

标签选择器的基本格式

<style type="text/css">
    选择器{
        属性: 值;
    }
</style>

选择字体倾斜，快捷键fs + Tab

font-style: italic;      ###字体倾斜

选择字体粗细

font-weight: bold;

设置字体大小，快捷键fs + Tab

font-size: 12px;

设置字体样式，他可以设置多个字体样式，用逗号隔开，系统默认会使用第一个字体，如果你设置的首个字体系统没有安装该字体，那么他就会使用第二个，如果第二个也没有，他就会使用默认自带的字体，如果想给系统英文和中文单独设置两个字体，可以将英文字体设置在前面，因为英文字体不包含中文

font-family: '微软雅黑','宋体';

上面四个属性可以用一行缩写，前两个style和weight可以省略和位置互换，后两个size和family则相反。

font: oblique bold 10px '宋体';

text-decoration文本装饰，有下滑线，删除线，上滑线 text-align文本水平对其左，居中，右 text-indent文字缩进，默认单位em color设置文本颜色，赋值的方式1.英文单词、2.rgb、3.rgba、4.十六进制、5.十六进制的缩写

color: blue;

ID选择器 id选择器不同于标签选择器，

1.  ID选择器是在前面要加上‘#’号，
2.  id的命名规则是必须以数字或者下划线开头，
3.  他可以包含字母、数字和下划线，他不能跟已有的标签重复。
4.  在企业开发中，id一般是留给js控制使用的，为了避免这样的误解，尽量使用类选择器

类选择器跟id差不多命名规则，类选择器在前面要加上‘.’，一个标签可以绑定多个类，写法是用空格隔开，实例class="类名1  类名2" 标签选择器   html标签名称  如：a id选择器    # + id名称  如：#a123 类选择器    . + 类名称  如：.a123 后代选择器   只修改父元素里的子元素的所有标签，用空格隔开 例如 #a123 .b123     只修改id‘a123’下的类b123所有内容 子元素选择器  用大于号作为连接符，它只会选择特定的一个元素    例如 #a123>.b123    只修改id‘a123’下的类b123单个元素 交集选择器：只修改两个元素相交的部分，格式为直接将两个标签挨着就行   例如  #a123>.b123     只修改必须包含id‘a123’下和类b123两个的元素 并集选择器   修改所有包含两个或者单个选择器的元素,用逗号隔开   例如 #a123,.b123   修改包含所有id‘a123’下和类b123其中一个或者两个的元素 相邻兄弟选择器   循环修改相邻紧跟的那一个标签，使用加号作为连接   例如#a123+.b123    循环修改类b123的那个标签，a123和b123是同级关系 通用兄弟选择器   循环修改相邻的所有标签，使用‘\`’作为连接    例如：#a123\`.b123循环修改类b123的所有标签，a123和b123是同级关系 序选择器：书写格式：p:first-child，含义为修改同级别的第一个p标签

1.  first-child   修改同级别的第一个标签
2.  first-of-type   修改同级别同类型的第一个标签
3.  last-child  修改同级别的最后一个标签
4.  last-of-type  修改同级别同类型的最后一个标签
5.  nth-child(n)  修改同级别的第n个标签
6.  nth-of-type(n)   修改同级别同类型的第n个标签
7.  nth-last-child(n)  修改同级别的倒数第n个标签
8.  nth-last-of-type(n)  修改同级别同类型的倒数第n个标签
9.  only-child   修改父元素只有一个的标签
10.  only-of-type  修改父元素中同类型唯一的一个标签

上面的n还有一些高级玩法，nth只会在同级别执行一次，我们可以用公式让它在同级别循环执行

1.    nth-child(odd)     循环修改同级别的序号为单数的标签
2.    nth-child(even)    循环修改同级别的序号为双数的标签
3.    nth-child(xn+y)    公式是x乘以n加上y，n从0开始想上递增+1，x和y为用户自定义的数字，循环修改同级别的序号为公式的结果的标签

同级别的第一个标签是id=1和id=3，同级别和同类型的p标签是id=2和id=3

<h2 id='1'>aaaaaaa</h2>
<p id='2'>我是第一行</p>
<p>我是第一行</p>
<p>我是第一行</p>
<p>我是第一行</p>
<p>我是第一行</p>
<div>
    <p id='3'>我是第一行</p>
    <p>我是第一行</p>
    <p>我是第一行</p>
    <p>我是第一行</p>
    <p>我是第一行</p>
</div>
<p>我是第一行</p> 
<p>我是第一行</p>

属性选择器： \[attribute\]       根据指定标签找对应的属性，然后设css 例如p\[class\]就可以更改下面两个p标签，因为他们两个都有class属性

<p class='a1'>我是第一行</p>
<p class='a2'>我是第二行</p>

\[attribute=value\]  根据指定标签找对应的属性，该属性的值必须和value相等才会设置css \[attribute=value\]     css2      和   \[attribute^=value\]   css3是都是匹配属性值以value开头的，然后设置css，区别是css2的只能识别这种‘value-abc’用横杠隔开的，css3只要是value开头的都可以识别 \[attribute$=value\]   css3       修改以value结尾的属性值的标签CSS \[attribute\`=value\]   css2   和  \[attribute\*=value\]     css3都是匹配值中包含的value的值，不同的是css2只能匹配空格隔开的，比如 abc value abc，而css3可以配置只要包含了value就行，由此可见后者更强大   **伪元素选择器**

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