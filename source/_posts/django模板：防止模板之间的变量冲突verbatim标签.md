---
title: Django模板：防止模板之间的变量冲突verbatim标签
tags: [django,python]
id: '199'
categories:
  - - 计算机编程
abbrlink: 9d5bc76b
date: 2018-10-24 15:23:13
---

当我们使用两个不同模板的，他们可能会跟django自带的DTL模板冲突，例如{ % %}、{ { } }，为了避免这样的事情发生，我们可以使用verbatim标签，它就不会执行标签之间的语法，转交给其他模板执行避免冲突

{ % verbatim %}
{ { if } } sss{ { if } }
{ % endverbatim %}      ###index.html