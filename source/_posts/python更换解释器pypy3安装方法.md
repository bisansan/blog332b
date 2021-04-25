---
title: Ubuntu16.04安装Python解释器PyPy3安装方法
tags: [ubuntu,python,pypy,linux]
id: '245'
categories:
  - - 计算机编程
abbrlink: 16940ee
date: 2018-11-11 17:00:25
---

PYPY宣传比python官方快7倍，是不是真的呢？测试机器为阿里云1核2G内存40G硬盘，测试代码如下

def fib(x):
    if x<2:
        return x
    return fib(x-1)+fib(x-2)

if \_\_name\_\_ == '\_\_main\_\_':
    import time
    begin = time.time()
    print(fib(40))
    end = time.time()
    print(end-begin)

测试截图如下，确实有官方所说的七倍的效果‘提升’ ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2018/11/20181111163644.png) 下面来介绍一下安装教程，官方推荐Ubuntu来安装，我使用的是16.04版本，官网下载页面：[http://pypy.org/download.html](http://pypy.org/download.html) 由于阿里云的Ubuntu16.04版本自带官方python2和python3，我就直接卸载了，免得和PyPy冲突，推荐保留python2，他不会和我们的pypy3冲突 `apt remove python    ###卸载python2` `apt remove python3   ###卸载python3` `apt autoremove python   ###卸载python2相关文件` `apt autoremove python3   ###卸载python3相关文件` 1.下载pypy3 6.0安装包，它对应的是python3.5.3版本 `wget https://bitbucket.org/pypy/pypy/downloads/pypy3-v6.0.0-linux64.tar.bz2` `tar xf pypy3-v6.0.0-linux64.tar.bz2  ##解压` `mv pypy3-v6.0.0-linux64/ /usr/local/pypy3 ##移动到系统目录` `export PATH=$PATH:/usr/local/pypy3/bin  ##添加系统临时变量，添加永久系统变量，将这行代码复制到/etc/profile文件最后一行，我们就可以来用pypy3来直接执行文件` 2.安装对应的pip3，我们就可以用它来安装模块 `pypy3 -m ensurepip   ###安装pip3` `pip3 install -U pip wheel  ###升级到最新` 3.假如你要安装一个模块或者执行一个脚本 `pypy3  123.py   ###执行python脚本` `pip3 install xxxx   ###安装一个模块` `pip install mysql-connector-python     ###安装mysql数据库连接驱动`