---
title: Vue.js：vue-router基本使用
tags: []
id: '791'
categories:
  - - Vue.js
abbrlink: dec2749b
date: 2019-08-14 11:44:10
---

在路由中渲染插件和指定一个链接

```
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->

  <router-link to="/foo">Go to Foo</router-link>  

  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 --> 

 <router-view></router-view>
```

路由组件url之间的绑定方法

```
// 方法一：先引入组件，再指定组件
import Home from './views/Home.vue'
    {
      path: '/',
      name: 'home',
      component: Home
    }

// 方法二：直接指定组件
    {
      path: '/about/:id',
      name: 'about',
      component: () => import('./views/About.vue')
    }
```

动态路由配置

$route.params 返回路由参数

```
    {
      path: '/about/:id',
      name: 'about',
      component: () => import('./views/About.vue')
    }

//  当我们访问到/about/123这个url时
//  $route.params就等于{ "id": "111" }
```

**$route.query** 返回查询字符串

更多api参考下面，例如当前绝对路径、网址和hash等等

[https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1](https://router.vuejs.org/zh/api/#%E8%B7%AF%E7%94%B1%E5%AF%B9%E8%B1%A1)

路由之间跳转

this.$router.replace(path) => 跳转到指定url链接，但是它不会在浏览器中产生记录

this.$router.push(path) => 跳转到指定url链接，并在history栈中添加一条新的记录。

this.$router.go(val) => 在浏览器history记录中前进(正数)或者后退（负数）val步，当val为0时刷新当前页面。当返回的页数不存在就会报错

this.$router.push(path) 等于 <router-link :to="...">

```
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' } })

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' } })
```

注意：如果提供了 path，params 会被忽略，上述例子中的 query 并不属于这种情况。取而代之的是下面例子的做法，你需要提供路由的 name 或手写完整的带有参数的 path：

嵌套路由

在路由中配置children选项，然后在主组件中加入<router-view/> 标签

```
//这是aa.vue组件
<template>
    <p>我是a里面的内容</p>
</template>

<script>
export default {
  name: 'aa'
}
</script>
```

```
 //路由配置  
 {
      path: '/about/:id',
      name: 'about',
      component: () => import('./views/About.vue'),
      children: [
        {
          // 当 /user/:id/aa 匹配成功，
          // aa.vue 会被渲染在 About.vue 的 <router-view> 中
          path: 'aa',
          component: () => import('./views/aa.vue')

        }
      ]
    }
```

```
//About.vue组件  
<div class="about">
    <h1>This is an about page</h1>
    <p> id是：{ { this.$route.params} }</p>
    <router-view></router-view>                                  //不要忘了这个标签
  </div>
```

当用户访问/user/:id/aa 和/user/:id/的区别如下

![](https://post.332b.com/wp-content/uploads/2019/08/2018194545-1024x321.jpg)

命名路由和命名视图

```
const router = new VueRouter({
  routes: [
    {
      path: '/user/:userId',
      name: 'user',
      component: User
    }
  ]
})
```

在定义路由时给他起个名字，就可以定义直接在视图导航中这样使用

```
<router-link :to="{ name: 'user', params: { userId: 123 } }">User</router-link>
```

也可以在js代码中这样用，它们是等价的

```
router.push({ name: 'user', params: { userId: 123 } })
```

命名视图中的用法

```
// 路由配置  
  {
      path: '/about/',
      name: 'about',
      component: () => import('./views/About.vue'),
      children: [
        {
          // 访问 /about 匹配成功，
          path: '/',
          components: {
            default: () => import('./views/aa.vue'),
            are: () => import('./views/bb.vue')
          }
        },
        {
          // 访问 /about/aa 匹配成功，
          path: 'aa',
          components: {
            default: () => import('./views/bb.vue'),
            are: () => import('./views/aa.vue')
          }
        }
      ]
    }
```

```
//About.vue 组件内容
 <div class="about">
    <h1>This is an about page</h1>
    <router-link to="/about/aa">链接到aa页面</router-link>
    <router-view></router-view>
    <router-view name="are"></router-view>
  </div>
```

![](https://post.332b.com/wp-content/uploads/2019/08/dfgdsfsdasas-1024x301.jpg)

别名和重定向

别名，当一个用户访问/a的时候，它实际是a组件，访问/b的时候，他还是a组件

```
{ 
path: '/a', 
component: A, 
alias: '/b'
 }
```

重定向 当你访问/a时，它将你重定向到/b

```
{ path: '/a', redirect: '/b' }
 { path: '/a', redirect: { name: 'foo' } }
```

更多参考

[https://github.com/vuejs/vue-router/blob/dev/examples/redirect/app.js](https://github.com/vuejs/vue-router/blob/dev/examples/redirect/app.js)