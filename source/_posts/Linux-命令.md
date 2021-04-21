---
title: Linux    命令
tags: []
id: '976'
categories:
  - - uncategorized
abbrlink: b0ba923a
---

## 文件修改

cmp diff 对比文件差异  
diffstat 读取diff的输出结果  
file 查看文件类型  
find（直接在文件中查找）locate（在数据库中查找） 查找文件  
updatedb 更新locate数据库  
indent 格式化C语言代码  
cut 截取指定范围的字符显示  
ln 建立软链接和硬链接  
cat（适合小文件，大文件打开慢） less（适合大文件，打开快，可以随意翻页） more（适合大文件，打开慢，只能向后翻页） 查看文件  
mktemp 建立缓存文件  
mv 移动文件或者目录  
od（不熟） 指令会读取所给予的文件的内容，并将其内容以八进制字码呈现出来  
paste 合并文件  
patch 命令用于修补文件  
rcp 复制远程文件到本地  
scp 复制本地文件到远程  
$ scp local\_file remote\_username@remote\_ip:remote\_folder  
rm 删除文件或者目录  
split 将单个文件分割成多个文件  
tee 将用户输入的内容保存到文件中  
tmpwatch 删除缓存文件（可以指定条件）  
touch 修改文件或目录时间属性，如果文件不存在，则会创造文件  
umask （不熟）命令指定在建立文件时预设的权限掩码  
cp 复制文件或者目录  
which 在环境变量$path设置的目录中，查找对应命令的执行文件位置  
$ which bash

/bin/bash

whereis 效果同上 ，不但会找出执行文件的位置，还有原始代码、二进制文件，或是帮助文件  
$ whereis bash

bash: /bin/bash /etc/bash.bashrc /mnt/c/Windows/System32/bash.exe /usr/share/man/man1/bash.1.gz

rhmask 加密或者解密文件  
awk 高级脚本匹配字符串，同类型有sed grep

## 文档编辑

col 过滤控制字符 例如：/n /t  
colrm 过滤指定行数控制字符  
comm 文本对比  
csplit 分割文件  
ed 简单文本编辑器  
egrep 查找字符串  
fgrep 查找文件里符合条件的字符串  
rgrep 递归查询字符串  
ex 以ex模式启动vim  
fmt fold 编排指定文件，例如：指定每行文件字数  
grep 查找字符串  
ispell 检查拼写，字典数据文件/usr/lib/ispell/english.hash  
jed(不熟) 用来编辑程序原始代码  
joe(不熟) 文本编辑器  
join 文本对比  
look 查找每行首字符  
pico 文本编辑器  
sed 多功能编辑文本  
sort 文本排序  
spell 检查拼写  
tr 替换字符  
expr（常用） 手工命令行计数器，用于在UNIX/LINUX下求表达式变量的值，一般用于整数值，也可用于字符串。  
uniq 删除相同行  
wc 统计数字  
let 表达式

## 文件传输

bye ftp模式下，中断ftp连接  
ftp ftp访问文件  
uuto uupick uucp uucico unix之间传送文件  
tftp tftp传输文件

## 磁盘管理

cd 进入目录  
df 统计磁盘使用情况  
dirs 显示目录路径  
dir 显示所有目录文件  
du 显示文件大小  
edquota 编辑用户或群组磁盘配额  
eject 卸载或退出设备，例如SD卡  
mkdir 建立文件夹  
mlabel（不熟） 命令用于设定磁盘的标签 (Label)  
mount 挂载文件或者分区  
unmount 卸载文件或分区  
pwd 显示工作目录  
quota（要安装工具） 命令用于显示磁盘已使用的空间与限制  
quotacheck 命令用于检查磁盘的使用空间与限制  
quotaoff 命令关闭磁盘空间限制  
repquota 命令用于检查磁盘空间限制的状态  
quotaon 命令用于开启磁盘空间限制  
rmdir 删除空目录  
rmt（不熟） 命令通过进程间通信远程控制磁带机  
stat (不熟) 命令用于显示inode内容  
tree（要安装工具） 命令用于以树状图列出目录的内容  
ls 显示所有文件内容  
lndir 命令用于连接目录内容（类似软链接）