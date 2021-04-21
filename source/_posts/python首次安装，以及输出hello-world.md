---
title: Python首次安装，以及输出hello world!
tags: []
id: '24'
categories:
  - - Python
abbrlink: b5fc856c
date: 2018-05-11 15:47:59
---

Python各版本官方windows下载地址 [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/) Python 官方安装包默认的添加的系统变量Path，解决CMD运行python出现内部或者外部命令，仅供参考

* * *

C:\\Users\\Administrator\\AppData\\Local\\Programs\\Python\\Python36\\Scripts\\;C:\\Users\\Administrator\\AppData\\Local\\Programs\\Python\\Python36\\

* * *

输入python进入交互模式，开始输出hello.world试试看 print('hello.world')   输出成功 print("hello.word")  输出成功 print('你好，世界')  输出成功 输入Ctrl-Z 或者 quit() 退出交互模式，再用pycharm输出代码试试

C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe C:/Users/Administrator/PycharmProjects/untitled/venv/Include/demo.py File "C:/Users/Administrator/PycharmProjects/untitled/venv/Include/demo.py", line 1 print('hello.world') ^ SyntaxError: invalid character in identifier

进程已结束,退出代码1 居然报错了，错误在第一行，我得问问度娘 经过仔细的核查发现，是括号用错了。。。。。。