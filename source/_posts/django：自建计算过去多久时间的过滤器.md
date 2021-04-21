---
title: Django：自建计算过去多久时间的过滤器
tags: []
id: '213'
categories:
  - - Django
abbrlink: 86ad84ca
date: 2018-10-26 15:36:10
---

上文链接：[https://post.332b.com/post/208.html](https://post.332b.com/post/208.html) 在文件中my\_filter.py写入下面代码

@register.filter
def time\_sinece(value):
    if not isinstance(value,datetime):
        return value
    now = datetime.now()
    timestamp = (now - value).total\_seconds()
    if timestamp < 60:
        return "刚刚发生"
    elif timestamp>= 60 and timestamp < 60\*60:
        aminutes = int(timestamp / 60)
        return "过去%s分钟" % aminutes
    elif 60\*60 <= timestamp < 60\*60\*24:
        ahour = int(timestamp/60/60)
        return "过去%s小时" % ahour
    elif 60\*60\*24 <= timestamp < 60\*60\*24\*30:
        aday = int(timestamp/60/60/24)
        return "过去%s天" % aday
    else:
        return value.strftime("%Y/%m/%d %H:%M")

在模板index.html中载入过滤器后，加入如下代码就可以实现我们想要的效果，它会显示当前过去了多久

{ { mytimetime\_sinece } }