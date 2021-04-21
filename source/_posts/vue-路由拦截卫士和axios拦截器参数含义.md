---
title: VUE 路由拦截卫士和Axios拦截器参数含义
tags: []
id: '832'
categories:
  - - uncategorized
abbrlink: 6da95e51
date: 2019-08-26 14:36:32
---

VUE路由拦截器

to,from,next 参数含义

```
to 和from共有参数
{
fullPath: "/about",     // 点击的路径
hash: "",
meta: {},           // 在路由中设置的meta字段
name: "about",   // 在路由中定义的名字
params: {},      // post或put提交的参数
path: "/about",  //路由中的路径
query: {}  // 查询字符串  /?aa=123&bb=456
}
```

注意next字段的使用方法

```
// 下面是正确的用法 
 if ( to.path === '/' ) {
    next({path: '/login'})
  } else {
  next()
}

// 这个也是正确的用法
next()

// 这个就是错误的用法，axios不能直接这样写，否则会无限循环
next({path: '/login'})

```

Axios拦截器

request请求拦截器 config 包含的接口

```
adapter: ƒ xhrAdapter(config)
baseURL: ""         //域名前缀
data: undefined         //提交
headers:
     Accept: "application/json, text/plain, */*"
     X-Custom-Header: "foobar"
maxContentLength: -1
method: "get"
timeout: 0
transformRequest: [ƒ]
transformResponse: [ƒ]
url: "http://jsonplaceholder.typicode.com/comments"
validateStatus: ƒ validateStatus(status)
xsrfCookieName: "XSRF-TOKEN"
xsrfHeaderName: "X-XSRF-TOKEN"
```

response请求拦截器 response接口

response 访问成功 接口代码

```
//  同request 中的 config
config: {url: "http://jsonplaceholder.typicode.com/comments", headers: {…}, baseURL: "", transformRequest: Array(1), transformResponse: Array(1), …}
// 下载获取到的json数据
data: (500) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, …]
//  得到的回话头
headers: {pragma: "no-cache", content-type: "application/json; charset=utf-8", cache-control: "public, max-age=14400", expires: "Fri, 23 Aug 2019 10:58:41 GMT"}
//  请求配置
request: XMLHttpRequest {onreadystatechange: ƒ, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}
//  请求状态码
status: 200
//  请求状态码文本
statusText: "OK"
```

response error访问错误 接口代码

```
//  提取方法 error.respose
//  配置代码
config: {url: "/1111/aaa", headers: {…}, baseURL: "", transformRequest: Array(1), transformResponse: Array(1), …}

// 获取的html源码
data: "<!DOCTYPE html>↵<html lang="en">↵<head>↵<meta charset="utf-8">↵<title>Error</title>↵</head>↵<body>↵<pre>Cannot GET /1111/aaa</pre>↵</body>↵</html>↵"

// 会话头
headers: {content-security-policy: "default-src 'none'", x-content-type-options: "nosniff", connection: "keep-alive", x-powered-by: "Express", content-length: "147", …}

//  请求
request: XMLHttpRequest {onreadystatechange: ƒ, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}

//  会话装状态
status: 404

//  错误文本
statusText: "Not Found"
```