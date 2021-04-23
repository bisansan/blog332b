---
title: ubuntu18.04  python3 和3.7 虚拟环境
tags: [python,ubuntu]
id: '648'
categories:
  - - 计算机编程
abbrlink: 1a63df8e
date: 2019-08-11 18:32:54
---

为什么需要虚拟环境？因为ubuntu很多模块已经依赖了系统自带python，如果我们也使用自带环境，可能会导致系统混乱，使用虚拟环境是最保险的

安装虚拟环境

```
apt-get install python3-venv python3-dev python3-pip
```

创建虚拟环境

```
python3 -m venv newName
```

newName:虚拟环境名称

进入虚拟环境目录激活

```
source bin/activate 
```

退出虚拟环境

```
deactivate
```

Python3.7环境如下

```
sudo apt install python3.7 python3.7-dev python3.7 
python3.7  -m venv newName   #创建python3.7环境
```

[https://www.jianshu.com/p/936dce766c66](https://www.jianshu.com/p/936dce766c66)