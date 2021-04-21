---
title: VUE-CLI3  全局变量模块导入方法
tags: []
id: '723'
categories:
  - - Vue.js
abbrlink: 7750a09b
date: 2019-07-22 17:32:20
---

新建myglobal.js，这样写入代码

```
function globalfunc () {
}   //这里是函数

let globalvariable = {
  static_file: './static/'
}   //这里是属性，可以存储一些公共变量

export default {
  globalfunc,
  globalvariable
}
```

在main.js导入，让它成为全局变量

```
import myglobal from './myglobal'
Vue.prototype.$myglobal = myglobal
```

在VUE模板中的使用方法

```
<script>
     this.$myglobal.globalvariable.static_file  //引入全局变量
     this.$myglobal.globalfunc()      //引入全局函数
</script>
```