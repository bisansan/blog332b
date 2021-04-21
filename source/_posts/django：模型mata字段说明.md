---
title: DJango：模型MATA字段说明
tags: []
id: '271'
categories:
  - - Django
date: 2018-11-13 15:07:58
---

class models(models.Model): class Mate: db\_table = 'db\_name' ordering = \['id','user'\] db\_table 这个指模型映射到数据库中的表名，默认是使用模型的名次 ordering 对指定数据进行排序，如果要反序列显示，就在前面加个负号‘-’，例如ordering = \['-id','user'\]