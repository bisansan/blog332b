---
title: ubuntu 安装VUE并配置多版本管理
tags: []
id: '813'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - Vue.js
abbrlink: a5f93eec
date: 2019-08-15 12:03:36
---

`nvm（Node Version Manager）`是一个用来管理`node`版本的工具。我们之所以需要使用`node`，是因为我们需要使用`node`中的`npm(Node Package Manager)`，使用`npm`的目的是为了能够方便的管理一些前端开发的包！`nvm`的安装非常简单，步骤如下：

1.  到这个链接下载`nvm`的安装包：`https://github.com/coreybutler/nvm-windows/releases`。
2.  然后点击一顿下一步，安装即可！
3.  安装完成后，还需要配置环境变量。在`我的电脑->属性->高级系统设置->环境变量->系统环境变量->Path`下新建一个，把`nvm`所处的路径填入进去即可！
4.  打开`cmd`，然后输入`nvm`，如果没有提示没有找不到这个命令。说明已经安装成功！
5.  `Mac`或者`Linux`安装`nvm`请看这里：`https://github.com/creationix/nvm`。也要记得配置环境变量。

`nvm`常用命令：

1.  `nvm install node`：安装最新版的`node.js`。nvm i == nvm install。
2.  `nvm install [version]`：安装指定版本的`node.js` 。
3.  `nvm use [version]`：使用某个版本的`node`。
4.  `nvm list`：列出当前安装了哪些版本的`node`。
5.  `nvm uninstall [version]`：卸载指定版本的`node`。
6.  `nvm node_mirror [url]`：设置`nvm`的镜像。
7.  `nvm npm_mirror [url]`：设置`npm`的镜像。

替换npm源镜像为国内淘宝镜像

```
# 查看镜像地址
npm get registry

# 设置成淘宝镜像
# npm
npm config set registry http://registry.npm.taobao.org/
# yarn
yarn config set registry http://registry.npm.taobao.org/ 
# 原版
npm config set registry https://registry.npmjs.org/
```

安装vue-cli3.0

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
# 查看版本
vue --version
```