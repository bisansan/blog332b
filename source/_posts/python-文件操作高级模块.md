---
title: python 文件操作高级模块
tags: []
id: '842'
categories:
  - - uncategorized
abbrlink: c5346ab1
---

警告：即使是更高级别的文件复制功能（[`shutil.copy()`](https://docs.python.org/zh-cn/3.7/library/shutil.html#shutil.copy)， [`shutil.copy2()`](https://docs.python.org/zh-cn/3.7/library/shutil.html#shutil.copy2)）也无法复制所有文件元数据。

在POSIX平台上，这意味着文件所有者和组以及ACL都会丢失。在Mac OS上，不使用资源分支和其他元数据。这意味着资源将丢失，文件类型和创建者代码将不正确。在Windows上，不会复制文件所有者，ACL和备用数据流。

linux shell查看文件的元数据 metadata

```
stat test1.txt

# 文件：test1.txt
# 大小：13        块：8          IO 块：4096   普通文件
# 设备：802h/2050dInode：2234255     硬链接：1
# 权限：(0664/-rw-rw-r--)  Uid：( 1000/    witt)   Gid：( 1000/    witt)
# 最近访问：2019-09-10 17:28:03.153571882 +0800
# 最近更改：2019-09-10 17:27:46.825308133 +0800
# 最近改动：2019-09-10 17:27:46.825308133 +0800
# 创建时间：-
```

**copyfileobj(fsrc, fdst, length=16\*1024)**： 将fsrc文件内容复制至fdst文件，length为fsrc每次读取的长度，用做缓冲区大小

*   fsrc： 源文件
*   fdst： 复制至fdst文件
*   length： 缓冲区大小，即fsrc每次读取的长度

```
import shutil 
f1 = open("file.txt","r") 
f2 = open("file_copy.txt","a+") 
shutil.copyfileobj(f1,f2,length=1024)
```

_follow\_symlinks = True_

这个参数的作用是，当为false时，你想复制的文件为软链接那就复制这个软链接到目标目录，如果是True，就直接复制这个文件，默认是Ture，下面的函数中，大部分都有这个

**copyfile(src, dst)**

复制文件到目标目录，如果文件已存在会被覆盖

src和dst相同会引发错误SameFileError，如果src或dst路径错误引发FileNotFoundError

**copymode(src, dst)**

复制文件权限，不会修改文件

**copystat(src, dst)**

复制元数据 metadata，不会修改文件