---
title: Django：Memcached缓存系统
tags: [django,Memcached]
id: '398'
categories:
  - - 计算机编程
abbrlink: 4b573984
date: 2018-12-14 17:36:30
---

memcached 什么足 memcached: I 1. memcached之前是danga的一个项目，最早是为LiveJoumal服务的，当初设计师为了加速LiveJournal访问速度而幵发的，后来 被很多大型项目采用。官网是www.danga.com或者是memcached.org 2. Memcached是一个高性能的分布式的内存对象缓存系统，全世界有不少公司采用这个缓存项目来构建大负载的网站，来分担数据 库的压力。Memcached是通过在内存里维护一个统一的巨大的hash表，memcached能存储各种各样的数据，包括图像、视频、 文件、以及数据库检索的结果等。简单的说就是将数据调用到内存中，然后从内存中读取，从而大大提髙读取速度。 3. 哪些情况下适合使用Memcached :存储验证码（图形验证码、短信验证码）、登录session等所有不是至关重要的数据。 安装参考[http://www.runoob.com/memcached/window-install-memcached.html](http://www.runoob.com/memcached/window-install-memcached.html) 3. 可能出现的问题： 。提示你没有权限：在打幵cmd的时候，右键使用管理员身份运行。 。提示缺少 pthreadGC2.dll 文件：将 pthreadGC2.dll 文件拷贝到 windows/System32 . 。不要放在含有中文的路径下面。 4. 启动 memcached : -d :这个参数是让memcached在后台运行。 -m :指定占用多少内存。以M为单位，默认为64M。 -p :指定占用的端口。對认端口是11211 -l :哪些ip地址可以链接 linux可以通过usr/bin/memcached执行带有参数的命令，如果正在运行，可以通过ps auxgrep memcached来查看进程ID来杀掉 telnet操作memcached      `telnet 127.0.0.1 11211`    IP和端口号 set       一个key对应一个值，如果这个key存在就会被覆盖  `set key 0(是否压缩) 60（保存时间秒） 7（字符长度）` get     获取一个key的值 delate   删除一个key的值 add    添加一个key，如果这个key存在侧会报错 flash\_all      删除和清空所有值 incr      让值相加，值必须为数字 decr    让值相减，值必须为数字 stats     查看memcached状态 STAT curr\_items 0  key和值的总数 STAT total\_connections 4   从开启到现在的总共连接数 STAT curr\_connections 1   当前连接数，默认最大连接数为1024

## Python   操作memcached

pip install python-memcached，在代码中import memcache 连接单个服务器

mc = memcache.Client(\['127.0.0.1:11211'\],debug=True)

连接多个服务器，达到分布式效果，它会根据自己的算法，随机将值存储到某个服务器

mc = memcache.Client(\['127.0.0.1:11211','192.168.1.1:11211'\],debug=True)

添加一个值，如果不设置time，它默认是0

mc.set('username','pingg',time=120)

添加多个值，值以字典的形式添加进去

mc.set\_multi({
    'ping':'双方都',
    'lop':'的双方都'
},time=120)

获取一个值

username = mc.get('username')

删除一个值

mc.delete('ping')

对值进行相加，如果没有传入delta默认加1

mc.incr('age',delta=10)

## Django连接memcached

setting.py文件输入下面可以连接memcached

CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
        'LOCATION': \[
            '127.0.0.1:11211',
            '192.168.1.1:11211'
        \]
    }
}

views.py引用模块

from django.core.cache import cache

views.py在视图函数中添加值

cache.set('username','zhiliao',100)

获取一个值

cache.get('username')

自定义django储存值的规则

def KEY\_FUNCTION(key, key\_prefix, version):
    return 'django:'+key
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcachedCache',
        'LOCATION': \[
            '127.0.0.1:11211',
        \],
        'KEY\_FUNCTION':KEY\_FUNCTION
    }
}

如果你觉得定个函数很麻烦，也可以用lambda一行代码来代替

lambda key, key\_prefix, version:'django:'+key