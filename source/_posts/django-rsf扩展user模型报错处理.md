---
title: django RSF扩展USER模型报错处理
tags: [django,python,Django Rest Framework]
id: '718'
categories:
  - - 计算机编程
abbrlink: c7b478
date: 2019-07-17 15:58:01
---

Django Rest Framework

```
'User' object has no attribute 'tracks'
```

使用扩展的方法是onetoone，需要注意的两个地方是下列地方

1.related\_name必须和Serializer里面的字段一样

2.对于onetoone，不要使用many=True，否则就会报错， many=True 适用于多对多

```
class UserExtensionSerializer(serializers.ModelSerializer):
    class Meta:
        model = UserExtension
        fields = ['birthday', 'telephone']

class accountDetailSerializer(serializers.ModelSerializer):
    user_detail = serializers.StringRelatedField(read_only=True)   #这里不要使用many=True
    class Meta:
        model = User
        fields = [
            "username",
            "email",
            "first_name",
            'is_superuser',
            'is_staff',   #是否是员工
            'is_active',   #账户是否是正常状态
            'date_joined',  #添加日期
            'user_detail',
        ]
```

```
class UserExtension(models.Model):
    user = models.OneToOneField(User,on_delete=models.CASCADE,related_name='user_detail')
    birthday = models.DateField(null=True,blank=True)
    telephone = models.CharField(max_length=14,null=True)
```