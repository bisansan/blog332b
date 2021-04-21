---
title: shell  定义变量和传参数学习篇(1)
tags: []
id: '925'
categories:
  - - uncategorized
abbrlink: 5f4c4605
date: 2020-04-21 10:50:42
---

1\. 定义和输出变量

```
# 定义变量
your_name='witt'

# 输出变量方法一
echo '输出变量(方法一)your_name：'
echo $your_name

# 输出变量方法二
echo '输出变量(方法二)your_name'
echo ${your_name}
```

2.只读变量和删除变量

```
# 创造变量并赋值
your_name='witt'

# 声明变量是只读变量
readonly your_name
echo your_name

# 更改只读变量值会报错
your_name='my_name'
echo your_name

# unset 删除变量
# unset 删除只读变量会报错
unset your_name
```

3.单双引号，截取字符串，获取字符串长度

```
your_name='witt'

my_name='lin'

# 单引号和双引号区别
echo 'your name is $your_name \n ‘OK’'
echo 'your name is ${your_name} \n \’ok\‘'
echo "your name is $your_name \n \'OK\’"
echo "your name is ${your_name} \n \"OK\""

# 获取变量字符长度
echo ${ {your_name}

# 截取字符串
echo ${your_name:0-2:4}

##############################
# your name is $your_name \n ‘OK’
# your name is ${your_name} \n \’ok\‘
# your name is witt \n \'OK\’
# your name is witt \n "OK"
# 4
# tt
```

4.定义数组和多行注释

```
# 定义一个数组
your_list1=('123' '2222' 'string1')

your_list2=(
    '11111111'
    '222255666'
    'aereyrey'
)

# 获取数组的某个值
echo ${your_list1[1]}

# 获取数组的长度
echo ${ {your_list1[@]}
# 将@改成*也可以获取

# 获取数组某个元素的长度
echo ${ {your_list1[2]}

# 多行注释
:<<EOF
我是第一行内容
我是第二行内容
EOF
```

5.传递参数

```
# 获取传递参数
echo "首个参数为文件本身： $0";
echo "参数一： $1";
echo "参数二： $2";
echo "参数总个数： $#"
echo "将所有参数转换单字符串一： $*"
echo "将所有参数转换单字符串二： $@"
echo "返回当前脚本进程id号：$$"
echo "返回后台运行的最后一个进程id号：$!"
echo "shell使用的当前选项：$-"
echo "显示脚本最后命令的退出状态（0代表无错误）：$?"

# 获取所有参数 $* 和 $@区别
# $* 在双引号输出是指将多个元素传递一个元素 ‘var1 var2 var3’
echo "$*"

# $@ 而它则相反‘var1‘ ’var2‘ ’var3’
echo "$@"
```