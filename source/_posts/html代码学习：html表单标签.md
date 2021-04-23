---
title: HTML代码学习：HTML表单标签
tags: [html]
id: '415'
categories:
  - - 计算机编程
abbrlink: d3122da2
date: 2018-12-21 22:19:55
---

input标签 明文输入框text

<input type="text">

暗文输入框password

<input type="password">

单选项radio，默认情况下是不会互斥的，设置了相同的name属性才会是单选，checked="checked"是默认选择一个值

<input type="radio" name="good">男
<input type="radio" name="good">女
<input type="radio" name="good" checked="checked">保密

多选项checkbox，它也可以使用checked="checked"是默认选择一个值

<input type="checkbox">篮球
<input type="checkbox">足球
<input type="checkbox">羽毛球

按钮button

<input type="button" value="按钮">

定义图像形式的提交按钮

<input type="image" src="11..jpg">

reset定义重置按钮。重置按钮会清除表单中的所有数据。

<input type="reset" />

hidden 定义隐藏字段。隐藏字段对于用户是不可见的。隐藏字段通常会存储一个默认值，它们的值也可以由 javascript 进行修改。

<input type="hidden" name="country" value="Norway" />

submit定义提交按钮。提交按钮用于向服务器发送表单数据。数据会发送到表单的 action 属性中指定的页面。

<form action="form\_action.asp" method="get">
Email: <input type="text" name="email" />
<input type="submit" />
</form>

lable标签：将文字和输入框绑定在一起，献给input定义一个id，然后在lable中用for关联到id完成绑定

<form action="">
    <lable for="user">账号：</lable><input type="text" id="user">
</form>

select属性是定义一个单选下拉框，option为选项，当数据太多的时候，我们可以通过optgroup来分类

<select>
    <optgroup label="分组选项1">
        <option>选项一</option>
        <option>选项二</option>
    </optgroup>
    <optgroup label="分组选项2">
        <option>选项三</option>
        <option>选项四</option>
    </optgroup>
</select>

textarea是一个多行文本框，clos定义列数，rows定义行数，随后可以定义行数和列数，但依旧还是可以无限向下输入

<textarea cols="3" rows="5">我是文本</textarea>