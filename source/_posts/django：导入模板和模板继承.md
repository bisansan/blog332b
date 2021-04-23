---
title: Django：导入模板和模板继承
tags: [django,python]
id: '223'
categories:
  - - 计算机编程
abbrlink: 97763a3b
date: 2018-11-01 15:32:23
---

导入模板是为了避免代码反复写，可以通过将反复使用的代码定义成一个模板，导入到另外一个模板，最常使用的是页头和页脚这些重复的页面

{ % include "header.html" %}     ##在同一templates目录下

在导入header.html父模板的时候，在访问子模板的时候，父模板可以使用子模板的变量 1.A子模板引用了B父模板之后，在访问A的时候，那么B就可以使用A里面的所有变量， 2.A和C子模板同时引用了B父模板，当B里面有A的变量，在访问C模板的时候，是无法使用A的变量的。 如果你是上面第2个情况，C子模板引用了B父模板，B父模板有A的变量，要想在C模板使用A的变量，那就必须给A变量定义一个值

{ % include "header.html"  with akey="zhilio" %}    ####假如这是C模板，#akey是A模板的变量，是无法直接使用，用with akey="xxx"就可以给它定义一个值

模板继承是子模板继承父模板的所有内容，语法如下，extends标签它必须放在模板的第一行

{ % extends "base.html"%}         #子模板继承父模板base.html的方法

模板继承block语法的用法，相当于在父模板中开了一个口子，可以在子模板中添加任意内容到父模板中去 在父模板中开一个口子的方法

<div calss="content" >
 { % block content %}
 { % endblock %}
</div>

在子模板中添加内容进去的方法，block里面添加的内容才会显示，其他不会显示

{ % extends "base.html"%}
{ % block content %}
我是添加的内容，嘻嘻
{ % endblock %}

如果父模板和子模板的{ % block content %}和{ % endblock %}都有添加的内容，那访问子模板的时候只会显示子模板的内容，如果要同时显示子和父模板的内容

{ { block.super  } }      ###在子模板添加这个就会显示父模板的内容