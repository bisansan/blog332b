---
title: 代码版本管理：GIT的基本操作
tags: []
id: '705'
categories:
  - - soft
    - GIT
abbrlink: 6ce3e36c
date: 2019-07-08 11:43:10
---

根据你的邮箱创建一个管理秘钥 ssh-keygen -t rsa -C "123@qq.com"

配置你本地的邮箱 git config --global user.email “you@example.com”

配置你本地的用户名 git config --global user.name “Your Name”

初始化当前目录为代码仓库 git init

添加一个仓库 git remote add demo https://e.coding.net/t/start.git

切换到当前分支 git checkout master

允许不相关的历史提交，就不会报错 git pull origin master --allow-unrelated-histories

提交当前代码master分支 git push origin master

第一次推送master分支的所有内容，如果不是第一次可以去掉U git push -u origin master

git Stashing（冻结和暂存）

查看暂存列表：git stash list

移除某个暂存： git stash drop \[name\]

恢复某个暂存：git stash apply \[name\] （ 这个不会删除暂存 ） git stash pop \[name\] （这个会删除对应的暂停）

fatal: refusing to [merge](https://www.centos.bz/tag/merge/) unrelated histories [https://www.centos.bz/2018/03/git-出现-fatal-refusing-to-merge-unrelated-histories-错误/](https://www.centos.bz/2018/03/git-出现-fatal-refusing-to-merge-unrelated-histories-错误/)