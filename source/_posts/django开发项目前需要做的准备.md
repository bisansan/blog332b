---
title: Django开发项目前需要做的准备
tags: [django,python]
id: '603'
categories:
  - - 计算机编程
abbrlink: 6dfa40a3
date: 2019-03-28 15:59:43
---

1.生成pip环境依赖模块的版本号，方便打包到生产环境中 生成requirements.txt文件 pip freeze > requirements.txt 安装requirements.txt依赖 pip install -r requirements.txt     2.写JS规范，例如JQ、VUE等等js库要写在header里面，当前的页面js写在body后面，这样可以最大的减少错误的发生     3.django和vue.js 2.0模板之间的' { { var } }' 冲突推荐的解决办法 模板

<div id="app">
    <p>{\[ message \]}</p>
</div>

JS

var app = new Vue({
delimiters: \['{\[', '\]}'\],
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})

注意：还有其他方法，但是不推荐，不方便编写代码，具体可以百度，vue.js 1.0和2.0冲突解决方法不一样     4.配置mysql，连接器为第三方mysqlclient，官方的连接器mysql-connector-python

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'xfz',
        'HOST': '127.0.0.1',
        'USER':'root',
        'PASSWORD':'root',
    }
}

官方mysql-connector-python连接方式

DATABASES = {
    'default': {
        'NAME': 'user\_data',
        'ENGINE': 'mysql.connector.django',
        'USER': 'mysql\_user',
        'PASSWORD': 'password',
        'OPTIONS': {
          'autocommit': True,
        },
    }
}

    5.配置模板路径TEMPLATES选项中的dir可以配置路径，默认为当前目录的templates，如果是多层目录例如当前目录下的/xfz/templates目录，就可以这样设置

'DIRS': \[os.path.join(BASE\_DIR, 'xfz','templates')\]

    6.配置静态路径，这里有更详细的设置方法：[https://post.332b.com/post/226.html](https://post.332b.com/post/226.html) 在setting.py末尾添加如下代码即可，添加静态文件目录

STATICFILES\_DIRS=\[(os.path.join(BASE\_DIR,'front', 'dist'))\]

    7.设置时区 检查 ‘USE\_TZ’ 是否为 ture 打开状态，再设置TIME\_ZONE = 'Asia/Shanghai'中国亚洲上海 添加mysql的时间储存库方法  [https://post.332b.com/post/288.html](https://post.332b.com/post/288.html)