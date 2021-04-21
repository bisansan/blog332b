---
title: Python爬取百度图片简易教程
tags: []
id: '277'
categories:
  - - Python
  - - 技术分享
abbrlink: 23c0a8a4
date: 2018-11-13 18:08:57
---

简单的下载

import requests
img\_url = 'https://ss0.bdstatic.com/70cFuHSh\_Q1YnxGkpoWK1HF6hhy/it/u=1054065341,1883567039&fm=26&gp=0.jpg'
response = requests.get(img\_url)
print(response.content)        ###以文本的形式打印出get到的文件

模拟用户来下载图片

import requests
headers = {
    "User-Agent":"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36",
    "Referer":'https://image.baidu.com/search/index?tn=baiduimage&ipn=r&ct=201326592&cl=2&lm=-1&st=-1&fm=index&fr=&hs=0&xthttps=111111&sf=1&fmq=&pv=&ic=0&nc=1&z=&se=1&showtab=0&fb=0&width=&height=&face=0&istype=2&ie=utf-8&word=%E5%9B%BE%E7%89%87&oq=%E5%9B%BE%E7%89%87&rsp=-1',
}
url = 'https://ss0.bdstatic.com/70cFuHSh\_Q1YnxGkpoWK1HF6hhy/it/u=1054065341,1883567039&fm=26&gp=0.jpg'
response = requests.get(url,headers=headers)
print(response.content)
response = requests.get(url,headers=headers)
with open('text.jpg','wb') as f: ###将图片写入文件
f.write(response.content)

模拟用户下载一页的图片

import requests,re
page\_url = 'http://image.baidu.com/search/index?tn=baiduimage&ps=1&ct=201326592&lm=-1&cl=2&nc=1&ie=utf-8&word=%E7%8C%AB'
headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36",
        "Referer": 'https://image.baidu.com/search/index?tn=baiduimage&ipn=r&ct=201326592&cl=2&lm=-1&st=-1&fm=index&fr=&hs=0&xthttps=111111&sf=1&fmq=&pv=&ic=0&nc=1&z=&se=1&showtab=0&fb=0&width=&height=&face=0&istype=2&ie=utf-8&word=%E5%9B%BE%E7%89%87&oq=%E5%9B%BE%E7%89%87&rsp=-1',
    }
response = requests.get(page\_url,headers=headers)
response.encoding = 'utf-8'
html = response.text
text = re.findall(r'"thumbURL":"(.\*?)"',html)

for index,saveimg in enumerate(text):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36",
        "Referer": 'https://image.baidu.com/search/index?tn=baiduimage&ipn=r&ct=201326592&cl=2&lm=-1&st=-1&fm=index&fr=&hs=0&xthttps=111111&sf=1&fmq=&pv=&ic=0&nc=1&z=&se=1&showtab=0&fb=0&width=&height=&face=0&istype=2&ie=utf-8&word=%E5%9B%BE%E7%89%87&oq=%E5%9B%BE%E7%89%87&rsp=-1',
    }
    response = requests.get(saveimg, headers=headers)
    with open('%s.%s'% (index,saveimg.split('.')\[-1\]),'wb') as f:
        f.write(response.content)

    的