---
title: VUE-CLI3 中引入laydate日期选择插件
tags: [vuejs,javascript]
id: '721'
categories:
  - - 计算机编程
abbrlink: e09f509
date: 2019-07-22 17:26:36
---

在main.js里面我们这样做，addjs为js路径，func为该js成功加载完后执行的函数

```
Vue.prototype.$addjs = function (addjs, func) {
  let oHead = document.getElementsByTagName('HEAD').item(0)
  let oScript = document.createElement('script')
  oScript.type = 'text/javascript'
  oScript.src = addjs
  oHead.appendChild(oScript)
  oScript.onload = func
}
```

在模板中我们这样写

```
<template>
      <input type="text" id="test1">
</template>
  
<script> //script部分
beforeMount () {
    let after = function () {
      window.laydate.render({
        elem: '#test1'
      })
    }
    this.$addjs('js/laydate/laydate.js', after)    //前为js路径，可以是网址
  }
</script>
```

就这样easy的搞定了，是不是很轻松？