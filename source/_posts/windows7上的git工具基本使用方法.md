---
title: WINDOWS7上的GIT工具基本使用方法
tags: []
id: '664'
categories:
  - - soft
    - GIT
date: 2019-06-05 16:19:22
---

首次使用设置一下邮箱和用户名 git config --global user.email "you@example.com" git config --global user.name "Your Name"   初始化仓库 git init   添加文件 git add file   提交文件 git commit -m "一段简要说明"   查看被所有被修改过的文件 git status   查看某个文件（对比上次提交时的文件）那些内容被修改 git diff file

$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index d8036c1..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
Git is free software.
\\ No newline at end of file

index d8036c1..013b5bc 100644 两个git版本的哈希值，100表示普通文件，644表示文件权限 @@ -1,2 +1,2 前面是文件被改动前的文本行数区间，后面是被改动后的区间   git log 查看最近提交历史日志  

commit 77dd66fa1aee8843096c3223a6bad99254613e7c (HEAD -> master)
Author: witt zoom <tm332b@qq.com>
Date: Wed Jun 5 11:48:57 2019 +0800

second submit

commit a75bea7f4a07dc906afb9aa3fa094b2256a6c589
Author: witt zoom <tm332b@qq.com>
Date: Wed Jun 5 11:17:07 2019 +0800

this is the first submit

  git log --pretty=oneline 简要的显示最近提交历史日志   HEAD代表当前版本 HEAD^代表上一个版本 git reset --hard HEAD^ 回滚到指定上一个版本 git reset --hard a75bea7f4a07 回滚到指定版本，不用全写，它会自己寻找   回滚到指定版本，出现无法查看之前提交的版本，可以用git reflog来查看提交的命令历史   可以查看工作区和版本库里面最新版本的区别 git diff HEAD -- readme.txt   git checkout -- file可以丢弃工作区的修改： `$ git checkout -- readme.txt` 命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况： 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态； 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。 总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。   用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区   设置远程仓库 git remote add origin https://github.com/bisansan/demo.git 推送到远程仓库  git push -u origin master 如果设置出现：fatal: remote origin already exists. 就删除当前设置的远程仓库 git remote rm origin