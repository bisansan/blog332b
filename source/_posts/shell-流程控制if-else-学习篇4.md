---
title: Shell  流程控制if...else 学习篇(4)
tags: []
id: '952'
categories:
  - - uncategorized
abbrlink: cc166f12
date: 2020-05-14 18:03:23
---

1.if....else流程控制

```
#!/bin/bash

# shell 流程控制

# if else 示例
number1=12
number2=23 
if [ $number1 == $number2 ]
then
    echo "number1和number2相等"
elif [ `expr 36 + 2` == 38 ]
then
    echo "36 + 2相加的结果为38"
else
    echo "number1和number2不相等"
fi
```

2\. for ... in ...流程控制

3\. while 流程控制

```
# while ...
# 当不满足条件时退出无限循环
number3=1
while (( $number3<=10 ))
do
    echo "当前循环到数字：$number3"
    let "number3++"
done
```

4\. until 流程控制

```
# until ...
# 当条件满足时退出无限循环
number4=1
until (( $number4==3 ))
do
    echo "当前until循环到：$number4"
    let "number4++"
done
```

5.case ... in ...

```
# 可以输入不同的条件，执行不同的命令
echo '输入“爱”或“不爱”表示你对我的态度：'
read love
case "$love" in
    "爱")
    echo "谢谢你的爱"
    ;;
    "不爱")
    echo "我也跟你一样"
    ;;
    *)
    echo "你还没有表达你的态度呢"
    ;;
esac
```

6.continue退出当前循环，进入下一次循环；break终止整个循环