---
title: HTML基础：段落、标题、链接、图像
tags: [html]
id: '234'
categories:
  - - 计算机编程
abbrlink: ba2aae76
date: 2018-11-04 15:11:24
---

1、段落是通过<p>文字</p>来实现的，下面是示例 `<p>我是一个段落</p>` 2.标题是通过h1~h6来实现的，数字越大，在网页中显示的字体就越小，一个网页最多出现一个H1标签，否则会影响SEO搜索收录 `<h1>我是H1标签</h1>` `<h3>我是H3标签</h3>` `<h6>我是H6标签</h6>` 3.链接是指将用户从一个网址导向另一个网址，是通过a标签<a href="网址">链接显示文字</a>，他的属性有 target可以控制跳转,\_self不新建窗口直接跳转，\_blank新建窗口打开网页 title是显示鼠标悬停上面显示的文本 在<head>和</head>添加<base target=\_blank>，可以统一实现所有链接\_blank新建窗口打开网页效果，如果a标签中指定了target，那么就会执行a标签里面的target 假链接是指用户点击之后不会跳转的链接，通常有两种

1.  href="#"   这种会点击会导致网页回到顶部
2.  href="javascript:"    这种点击了，什么都不会发生

`<a href="www.baidu.com">点击进入百度</a>` a标签除了可以跳转到指定链接，还可以跳到当前页面指定位置，但得先给指定的位置指定一个id `<a href="#aaa">点击进入百度</a>` <p id="aaa">这里真好，嘻嘻</p> 4.在网页中图像是通过img标签来展示的，<img src="图片"/>，如果要制定上一级的路径可以这样指定src="../图片.img" 属性width来限制宽度，height来限制显示的高度， src是source的简写，中文意思是资源，手动制定高度和宽度可能会导致图片变形，单独制定高度或者宽度不会变形，但是会等比拉伸， title属性作用当鼠标悬停在图片，显示对图片的文本描述， alt标签作用是当图片资源失效或者无法显示的时候，会显示制定的文本 `<img src="tu.jpg" width=“600” height="600">` 5.下划线可以通过单标签`<hr />` 来表示，它叫做下划水平分割线 6.html注释一段文字方法`<!--这个是注释的文字-->` ,注释一段话的快捷键 Ctrl + / 7.<br />是指不另起一段换行，企业开发中很少用到br标签，企业中要使用到换行一般都是另起一个段落 home可以跳到一行的开头，end可以跳到一行的末尾，Ctrl + Alt + Ins可以新建一个html文件，ALT + 鼠标左键上下拖动可以让多行同时进行输入，Ctrl + D复制光标所在的那一行，Ctrl + X删除光标所在的那一行，Ctrl + Alt + T按下回车，可以给一段文本快速指定一个标签，编辑器-常规-勾选自动换行就可以超长文本自动换行