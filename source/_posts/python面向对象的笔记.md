---
title: 'Python:面向对象的笔记'
tags: []
id: '174'
categories:
  - - Python
abbrlink: 468a0607
date: 2018-10-23 11:28:18
---

class需要通过中间人`a = father()`来执行类，`a.name()`可以执行类里面的函数

class father:
    def name(self):
        print("goosd")
a = father()
a.name()

继承是指`class father`是`class son(father)`的父类，当子类没有函数名时就会向父类里面去查找，如过有就优先使用子类函数名，在子类中启动父类函数名的方法`father.篮球(self)`或者`super(son,self).篮球()` （优先使用后面）

class father:
    def 篮球(self):
        print("篮球")
    def 足球(self):
        print("足球")
    def 抽烟(self):
        print("抽烟")

class son(father):
    def 保健(self):
        #super(son,self).篮球()
        father.篮球(self)
        print("保健")
k = son()
k.保健()

函数的封装，

class ass:
    def \_\_init\_\_(self,name):
        self.ss = "good"
        print(self.ss,name)

a = ass("你好")

在一类里面的函数引用其他函数

class Talk(object):
    def \_\_init\_\_(self, name, age):
        self.name = name
        self.age = age
        self.info = None
    def checkAge(self):
        if self.age < 18:
            self.info = '未满十八岁'
        elif self.age < 40:
            self.info = '拼搏的时代'
        elif self.age < 70:
            self.info = '请注意身体'
        else:
            self.info = '年过七旬'
    def sayInfo(self):
        if self.info == None:
            self.checkAge()
        print(self.name, ":", self.info)

peo = Talk('li', 28)
peo.sayInfo()