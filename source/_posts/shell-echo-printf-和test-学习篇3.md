---
title: SHELL echo printf 和test   学习篇(3)
tags: [shell,linux]
id: '940'
categories:
  - - 系统运维
abbrlink: df2c992a
date: 2020-05-12 16:58:25
---

1.echo 使用大全

```
#!/bin/bash

# echo为输出命令

# 普通字符
echo '1111'

# 转义
echo "\"这是一段话'\""

# 变量
kk='1'
echo "$kk"

# 换行
echo -e "ok! \n" # -e 开启转义，使\n换行生效
echo "It is OK"

# 不换行
echo -e "not ok! \c" # -e 开启转义，使\c换行生效
echo "It is not ok!"

# 输出字符到文件
# 如果文件已存在，会覆盖
echo "it is not ok in text" > myfile.txt

# 单引号不转义或获取变量
name='admin'
echo '$name \n'

# 执行命令
echo `date`
```

![](https://post.332b.com/wp-content/uploads/2020/05/20200511145250.png)

2.prinf 使用大全

```
#!/bin/bash

# printf 输出命令
# printf format-string [arguments1 arguments2 ...]

# 标准模式
# %-4.2f   总共输出4i位i数字，其中两位是小数，-符号代表左对齐，没有就是右对齐
printf "%-10s %-10i %-4.2f \n" 周杰伦 12 10.32453425
printf "%-10s %-10i %-4.2f \n" 周杰伦 12 10.32453425
printf "%-10s %-10i %-4.2f \n" 周杰伦 123456789010 101.32453425
printf "%-10s %-10i %-4.2f \n" 周杰伦覆盖不到返回给 12 10111111111111111.32453425

# 输出变量
var1=1
var2='string'
var3="val: $string"
# 直接输出变量
printf "%20s \n" $var2
# 在字符串中输出变量
printf "%20s \n" "val: $var2"
```

![](https://post.332b.com/wp-content/uploads/2020/05/20200511153815.png)

3.test 使用方法

a.判断数字

```
#!/bin/bash

# test 测试命令

# 测试两个数是否相等
# -eq:==  -ne:!=  -gt:>  -ge:<=  -lt:<  le:<=
number1=100
number2=200
if test $[number1+100] -eq $[number2]
then
    echo "两个数相等"
else
    echo "两个数不相等"
fi
```

b.判断字符

```
#!/bin/bash

# test 测试命令

# 测试两个数是否相等
# -eq:==  -ne:!=  -gt:>  -ge:<=  -lt:<  le:<=
number1=100
number2=200
if test $[number1+100] -eq $[number2]
then
    echo "两个数相等"
else
    echo "两个数不相等"
fi

# 测试字符串
# 判断条件：=  !=  -z(字符串长度为空)  -n(字符串长度不为空)
string1="111"
string2="222"
if test $string1 = string2
then
    echo "字符串相等"
else
    echo "字符串不相等"
fi

# 测试字符是否为空
if test -z $string1
then
    echo "字符串为空"
else
    echo "字符串不为空"
fi
```

c.判断文件

![](https://post.332b.com/wp-content/uploads/2020/05/20200511174553.png)

```
#!/bin/bash

# test 测试文件
# -e 文件是否存在  -r 是否可读 -w 是否可写 -x是否可执行
# -s 文件至少有一个字符  -d 文件存在且为目录
# -f 文件存在且为普通文件  -c 文件存在且为字符型特殊文件（例如键盘）
# -b 文件存在且为块特殊文件（例如硬盘）

# 获取当前目录
abc=`pwd`
# 将路径保存到o.txt
echo "这个目录为：$abc" > $abc'/o.txt'

# 检测文件是否存在
if test -e $abc'/o.txt'
then
    echo "文件已存在"
else
    echo "文件不存在"
fi
```

4.test 多个条件拼接

*   ! (非) 优先级最高
*   \-a (与) 优先级中
*   \-o (或) 优先级最低

```
#!/bin/bash

# test 测试文件
# -e 文件是否存在  -r 是否可读 -w 是否可写 -x是否可执行
# -s 文件至少有一个字符  -d 文件存在且为目录
# -f 文件存在且为普通文件  -c 文件存在且为字符型特殊文件（例如键盘）
# -b 文件存在且为块特殊文件（例如硬盘）

# 获取当前目录
abc=`pwd`
# 将路径保存到o.txt
echo "这个目录为：$abc" > $abc'/o.txt'

# 多个条件示例
# 检测文件是否存在且文件不可以执行
if test -e $abc'/o.txt' -a ! -x $abc'/o.txt'
then
    echo "文件已存在且不可以执行"
else
    echo "文件不存在或文件可以执行"
fi
```