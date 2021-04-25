---
title: Shell    运算符 学习篇(2)
tags: [shell,linux]
id: '933'
categories:
  - - 系统运维
abbrlink: 8eb072d
date: 2020-04-24 21:38:03
---

1.加减乘除，取余，判断相对和不相等

```
# 相加
val=`expr 2 + 2`
echo "2+2结果为：$val"

# 减法
val=`expr 8 - 3`
echo "8-3结果为：$val"

# 乘法
val=`expr 3 \* 4`
echo "3x4结果为：$val"

# 除法
val=`expr 9 / 3`
echo "9÷3结果为：$val"

# 取余数
val=`expr 11 / 3`
echo "11÷3的余数为：$val"

# 赋值
exp1=12
exp2=10
val=`expr $exp1 = $exp2`
echo "赋值为：$val"

# 判断相等，相等返回true
exp1=12
exp2=10
val=`expr $exp1 == $exp2`
echo "两值测试是否相等：$val"

# 判断是否不想动，不想等返回ture
exp1=12
exp2=10
val=`expr $exp1 != $exp2`
echo "两值测试是否不相等：$val"

# [Running] bash "ssh/1.sh"
# 2+2结果为：4
# 8-3结果为：5
# 3x4结果为：12
# 9÷3结果为：3
# 11÷3的余数为：3
# 赋值为：0
# 两值测试是否相等：0
# 两值测试是否不相等：1
```

2.关系运算：大于，小于，大于或等于，小于或等于

```
# 关系运算符
val1=12
val2=7

# -eq 检测两个数是否相等
val=`$val1 -eq $val2`
echo "检测是否相等：$val"

# -ne 检测两个数是否不相等
val=`$val1 -ne $val2`
echo "检测是否不相等：$val"

# -gt 检测左边数是否大于右边
val=`$val1 -gt $val2`
echo "检测左是否大于右：$val"

# -lt 检测左边是否小于右边
val=`$val1 -lt $val2`
echo "检测左是否小于右：$val"

# -ge 检测左边是否大于或等于右边
val=`$val1 -ge $val2`
echo "检测左是否大于或等于右：$val"

# -le 检测左边是否小于或等于右边
val=`$val1 -le $val2`
echo "检测左是否小于或等于右：$val"
```

3.布尔运算符：或，与，非

```
# 布尔运算符
val1=12
val2=7

# -o 或 满足其中的一个条件就成立
if [ $val1 -eq $val2 -o $val1 -gt $val2 ]
then
    echo "val1比val2大或相等"
else
    echo "val1比val2小或相等"
fi

# -a 与 所有的条件都必须满足就成立
if [ $val1 -eq $val2 -a $val1 -gt $val2 ]
then
    echo "val1比val2大且相等"
else
    echo "val1比val2小或不相等"
fi

# ! 非 不满足当前条件就成立
if [ $val1 != $val2 ]
then
    echo "val1和val2不相等"
else
    echo "val1和val2相等"
fi
```

4.逻辑运算符

```
# 逻辑运算符
val1=12
val2=7

# && 逻辑上的and
if [[ $val1 -gt 100 && $val2 -gt 5 ]]
then
    echo "条件满足"
else
    echo "条件不满足"
fi

#  逻辑上的or
if [[ $val1 -gt 100  $val2 -gt 5 ]]
then
    echo "条件满足"
else
    echo "条件不满足"
fi
```

5.字符串运算符

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/04/screenshot-www.runoob.com-2020.04.24-21_37_21.png)

6.文件关系运算符

![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2020/04/screenshot-www.runoob.com-2020.04.24-21_35_01-721x1024.png)