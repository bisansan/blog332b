---
title: 完整的配置一个linux的前段开发gulp环境
tags: []
id: '629'
categories:
  - - JavaScript
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
date: 2019-04-10 15:23:14
---

linux 地址：[https://github.com/creationix/nvm](https://github.com/creationix/nvm) windows下载：[https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases) 执行命令curl

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh  bash

or Wget:

wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh  bash

注意：如果无法执行，请用安装wget和curl工具 安装完后重启一下就可以执行nvm命令，执行下面命令是全局 `export NVM_DIR="${XDG_CONFIG_HOME/:-$HOME/.}nvm"` `[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm`   查看所有node版本（推荐6.4版本）：[https://nodejs.org/zh-cn/download/releases/](https://nodejs.org/zh-cn/download/releases/) `nvm install 6.17.1` `nvm use 6.17.1` 接下来就可以用npm安装包了,下面是我的配置文件 [gulp.zip](https://post.332b.com/wp-content/uploads/2019/04/gulp.zip)