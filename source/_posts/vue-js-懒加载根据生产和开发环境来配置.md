---
title: VUE.js 懒加载根据生产和开发环境来配置
tags: [nodejs,javascript]
id: '807'
categories:
  - - 计算机编程
abbrlink: 1af25f95
date: 2019-08-14 16:13:34
---

开发环境不需要懒加载，客户端需要懒加载，为了避免来回切换麻烦，可以使用下面的方法

新建import-development.js和import-production.js文件

```
//import-development.js
module.exports = file => require('@/views/' + file + '.vue').default


//import-production.js
module.exports = file => () => import('@/views/' + file + '.vue')
```

在路由入口文件这样使用

```
const _import = require('./import-' + process.env.NODE_ENV)     
//  process.env.NODE_ENV  在vue cli3中使用有所改变
// 建议使用新的https://post.332b.com/blog/672.html


// 然后定义一个路由的方法
{
  path: '/login',
  component: _import('modules/login/login'),
  name: 'login',
  meta: {
    title: '登录'
  }
}
```