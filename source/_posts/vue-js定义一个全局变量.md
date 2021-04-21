---
title: VUE-JS 定义开发环境和生产环境全局变量
tags: []
id: '672'
categories:
  - - Vue.js
date: 2019-06-14 16:05:24
---

1.在项目目录新建一个.env文件，打开文件设置一个变量

```
#.env文件
VUE_APP_URL=http://www.baidu.com
```

注意前面的VUE\_APP\_是系统已经固定好的格式，后面的URL才是我们可以改变的部分

同时.env还有开发模式和生产环境，不同环境执行不同文件

普通通用环境.env（无论那个环境都一样）

开发环境.env.development（这个文件需要自己创建）

生产环境.env.production

2.在app脚手架中应用

```
#xxx.vue文件使用方法

<html>
<p>{ {url} }</p>
</html>


<script>
export default {
  name: 'HelloWorld',
  data:function(){
    url:process.env.VUE_APP_URL
  },
}
</script>
```