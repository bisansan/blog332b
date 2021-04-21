---
title: django rest framework api框架学习
tags: []
id: '709'
categories:
  - - django
    - Django Rest Framework
abbrlink: '60028424'
date: 2019-07-12 13:50:28
---

```
from django.db import models    #models.py

class Publisher(models.Model):
    name = models.CharField(max_length=32,verbose_name='名称',unique=True)
    address = models.CharField(max_length=128,verbose_name='地址')

    def __str__(self):
        return  self.name

    class Meta:
        verbose_name = "出版社"
        verbose_name_plural = verbose_name
```

定义API字段的方法

第一种像这样直接定义字段的名字，就像这样

```
from . import models      ###serializers.py文件
from rest_framework import serializers     ###serializers.py文件

class PubisherSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    name = serializers.CharField(max_length=32)
    address = serializers.CharField(max_length=128)

    def create(self, validated_data):
        return models.Publisher.objects.create(**validated_data)

    def update(self, instance, validated_data):
        instance.name = validated_data.get('name',instance.name)
        instance.address = validated_data.get('address',instance.address)
        instance.save()
        return instance
```

```
from . import models,serializers            ##views.py 
from rest_framework.response import Response
from rest_framework.decorators import api_view
from rest_framework import status

@api_view(['GET', 'POST'])
def publisher_list(request, format=None):
    """
    列出所有的出版社，或者创建一个新的出版社
    """
    if request.method == "GET":
        queryset = models.Publisher.objects.all()  # 所有的出版社
        s = serializers.PublisherSerializer(queryset, many=True)
        return Response(s.data)

    if request.method == "POST":
        # 创建出版社
        s = serializers.PublisherSerializer(data=request.data)
        if s.is_valid():
            s.save()
            return Response(s.data, status=status.HTTP_201_CREATED)
        else:
            return Response(s.errors, status=status.HTTP_400_BAD_REQUEST)

@api_view(['GET','POST','DELETE'])
def publisher_detail(request,pk):
    """
    获取，更新或删除一个实类
    """
    try:
        publisher = models.Publisher.objects.get(pk=pk)
    except models.Publisher.DoesNotExist:       #如果获取异常，就返回一个404的错误
        return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method == 'GET':
        s = serializers.PublisherSerializer(publisher)
        return Response(s.data)

    elif request.method == 'PUT':
        s = serializers.PublisherSerializer(status=status.HTTP_404_NOT_FOUND)
        if s.is_valid():
            s.save()
            return Response(s.data)
        return Response(s.errors,status=status.HTTP_400_BAD_REQUEST)

    elif request.method == "DELETE":
        publisher.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

第二种根据模型来选取想要的字段，（ 下面两个文件是一起的 ）

```
from . import models      ###serializers.py文件
from rest_framework import serializers     ###serializers.py文件
class PublisherSerializer(serializers.ModelSerializer):       
    class Meta:
        model = models.Publisher
        fields = (
            "id",
            "name",
            "address"
        )
```

```
from . import models,serializers     ###views.py文件 
from rest_framework.response import Response
from rest_framework.decorators import api_view
from rest_framework import status

def publisher_list(request):      
    if request.method == 'GET':
    queryset = models.Publisher.objects.all()
    serializer = serializers.PubisherSerializer(queryset,many=True)
    return Response(serializer.data)
    if request.method == 'POST':
        s = serializers.PubisherSerializer(data=request.data)
        if s.is_valid():
            s.save()
            return Response(s.data,status=status.HTTP_201_CREATED)
        else:
            return Response(s.errors,status=status.HTTP_400_BAD_REQUEST)
```

如果没有上面这些模块，你可能要像这样去编码代码

```
    # data = []
    # for i in queryset:
    #     p_tmp = {
    #         'name': i.name,
    #         'address': i.address
    #     }
    #
    #     data.append(p_tmp)

    # data = []
    # from django.forms.models import model_to_dict
    # for i in queryset:
    #     data.append(model_to_dict(i))

    # import json
    # return HttpResponse(json.dumps(data),content_type="application/json")

    # from django.core import serializers
    # data = serializers.serialize('json', queryset)
    #
    # return HttpResponse(data,content_type="application/json")

    # from . import serializers
    # queryset = models.Publisher.objects.all()
    # serializer = serializers.PubisherSerializer(queryset,many=True)
    # import json
    # return HttpResponse(json.dumps(serializer.data),content_type="application/json")
```

在URL路由中，可以这样去配置

```
from django.contrib import admin        ###urls.py
from django.urls import path,include,re_path
from apps.app001 import views
from rest_framework.urlpatterns import format_suffix_patterns

urlpatterns = [
    path('admin/', admin.site.urls),
    path('account/', include('apps.account.urls')),
    path('publishers/',views.publisher_list),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework')),
    re_path(r'publishers/(?P<pk>[0-9]+)/',views.publisher_detail)
]
```

视图函数 API VIEW

```
from . import models,serializers
from rest_framework.response import Response
from rest_framework.views import APIView
from rest_framework import status
from django.http import Http404
class PublisherList(APIView):
    def get(self,reuquest,format=None):
        queryset = models.Publisher.objects.all()       #查询所有信息

        s = serializers.PublisherSerializer(queryset,many=True)
        return Response(s.data)

    def post(self,request,format=None):
        s = serializers.PublisherSerializer(data=request.data)
        if s.is_valid():    #如果信息就执行
            s.save()
            return Response(s.data,status=status.HTTP_204_NO_CONTENT)
        return Response(s.errors,status=status.HTTP_400_BAD_REQUEST)


class PublisherDetail(APIView):
    def get_object(self, pk):
        try:
            return models.Publisher.objects.get(pk=pk)
        except models.Publisher.DoesNotExist:
            raise Http404

    def get(self,request,pk,format=None):
        publisher = self.get_object(pk)
        s = serializers.PublisherSerializer(publisher)
        return Response(s.data)

    def put(self,request,pk,format=None):
        publisher = self.get_object(pk)
        s = serializers.PublisherSerializer(publisher,data=request.data)
        if s.is_valid():
            s.save()
            return Response(s.data)
        return Response(s.errors,status=status.HTTP_400_BAD_REQUEST)

    def delete(self,request,pk,format=None):
        publisher = self.get_object(pk)
        publisher.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

混淆视图函数 MIXINS

```
class PublisherList(
                    mixins.ListModelMixin,
                    mixins.CreateModelMixin,
                    generics.GenericAPIView):

    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer

    def get(self,request,*args,**kwargs):
        return self.list(request,*args,**kwargs)

    def post(self,request,*args,**kwargs):
        return self.create(request,*args,**kwargs)


class PublisherDetail(mixins.RetrieveModelMixin,
                        mixins.UpdateModelMixin,
                        mixins.DestroyModelMixin,
                        generics.GenericAPIView):

    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer

    def get(self,request,*args,**kwargs):
        return self.retrieve(request,*args,**kwargs)

    def put(self,request,*args,**kwargs):
        return self.update(request,*args,**kwargs)

    def delete(self,request,*args,**kwargs):
        return self.destroy(request,*args,**kwargs)
```

混淆视图函数简写方式 MIXINS

```
class PublisherList(generics.ListCreateAPIView):
    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer

class PublisherDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer
```

权限管理认证

第一种、所有匿名和登录用户可以查询和修改

```
class PublisherList(generics.ListCreateAPIView):
    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer
    permission_classes = ()  ##所有匿名和登录用户可以查询和修改
```

第二种、所有匿名和登录用户可以查询和修改

```
class PublisherList(generics.ListCreateAPIView):
    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer
    permission_classes = (permissions.IsAuthenticated,)  ##所有匿名和登录用户可以查询和修改
```

第三章、 只有创建者才可以修改，所有匿名和登录用户可以查询

```
class PublisherList(generics.ListCreateAPIView):
    queryset = models.Publisher.objects.all()
    serializer_class = serializers.PublisherSerializer
    permission_classes = (permissions.IsAuthenticatedOrReadOnly, IsOwnerOrReadOnly)    ##只有创建者才可以修改，所有匿名和登录用户可以查询
    def perform_create(self, serializer):
        serializer.save(operator=self.request.user)  #重写创建方法，不然会报错
```