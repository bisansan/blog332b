---
title: Django模板：spaceless和autoescape标签去掉多余空格和关闭默认转义
tags: [django,python]
id: '196'
categories:
  - - 计算机编程
abbrlink: 1b5bb0bd
date: 2018-10-24 15:07:17
---

spaceless标签是把标签之间所有无用的空行去掉，浓缩成一行，但是它不会去掉<strong>到</strong>之间无用的空格

{ % spaceless %}
<p>
    <a href="url">url</a>
</p>
{ % endspaceless %}

之前是上面这个样子，用了之后就是这个样子 `<p> <a href="url">url</a> </p>` Django中的DTL模板已经默认开启了转义，例如将“<”转换成&lt;

text = {
    "baidu":"<a href=\\"www.baidu.com\\">百度</a>"
}
def index(request):
    return render(request,"index.html",context=text)    ####urls.py

{ { baidu } }     ####index.html

如果将这个字典的key值直接输入到网页就是这样 ![](https://gitee.com/wittzhang/pic332b/raw/master/wp-content/uploads/2018/10/20181024150256-300x38.png) 如果你使用了autoescape，那么它就会还原它本来的模样，将它变成超链接

{ % autoescape off %}
    { { baidu } }
{ % endautoescape %}         ####index.html