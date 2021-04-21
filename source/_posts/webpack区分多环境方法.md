---
title: webpack区分多环境方法
tags: []
id: '872'
categories:
  - - uncategorized
date: 2019-10-05 23:39:12
---

这个要使用到cross-env插件，先安装一下

```
npm install --save-dev cross-env
```

安装完之后，在package.json中这样设置

```
 "scripts": {
    "dev": "cross-env NODE_ENV=production webpack --mode production",
  }
```

当我们运行了npm run dev之后，就可以在Js中这样判断

```
console.log(process.env.NODE_ENV);

// 打印结果如下
// production
```

能设置环境变量以后，可以通过webpack-merge分离多个配置，例如开发、测试和生产环境等等

```
npm install webpack-merge -D
```