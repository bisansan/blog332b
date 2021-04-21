---
title: python 读取一个文件下面的所有文件和目录
tags: []
id: '853'
categories:
  - - Python
abbrlink: ec26267d
date: 2019-09-27 14:21:21
---

```
# 获取当前执行文件路径
filepath = os.getcwd()

# 文件循环
def fileloop(filepath):
    fileList = os.listdir(filepath)
    for i in fileList:
        # 如果是目录，就调用自身，继续执行
        if os.path.isdir(filepath + '/' + i):
            print('目录:', filepath+ '/' + i)
            fileloop(filepath + '/' + i)
        elif os.path.isfile(filepath + '/' + i):
            print('文件:', filepath + '/' + i)
        else:
            print('无法识别文件:', filepath + '/' + i)

fileloop(filepath)
```