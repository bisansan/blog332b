---
title: Python3格式化输出文本语法
tags: []
id: '26'
categories:
  - - Python
abbrlink: '88977851'
date: 2018-05-23 16:22:13
---

#### 示例下面代码，跟用户交互然后显示该用户资料

name = input("名字：") age = input("年龄：") job = input("工作：") home = input("家乡：") print("---------关于",name,"信息-------") print("姓名：",name) print("年龄：",age) print("工作：",job) print("家乡：",home) print("-----------结束---------------")

#### 第二种实现方式

name = input("名字：") age = input("年龄：") job = input("工作：") home = input("家乡：") info = """ ---------关于 %s 个人信息----------- 姓名：%s 年龄：%s 工作：%s 家乡：%s ---------结束---------------------- """ % (name,name,age,job,home) print(info) **%作为连接符，与上面的占位符 %s 关系依次对应，%s = string（字符串），%d = digit（数字），%f = flota（浮点数）** 格式化输出，只允许年龄填入数字修改后的代码 name = input("名字：") age = int(input("年龄：")) job = input("工作：") home = input("家乡：") info = """ ---------关于 %s 个人信息----------- 姓名：%s 年龄：%d 工作：%s 家乡：%s ---------结束---------------------- """ % (name,name,age,job,home) print(info)