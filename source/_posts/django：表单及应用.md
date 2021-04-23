---
title: Django：表单及应用
tags: [django,python]
id: '382'
categories:
  - - 计算机编程
abbrlink: 69f47e64
date: 2018-12-11 18:02:23
---

## 一.Django中的表单使用方法

HTML中的表单: 单纯从前端的html来说，表单是用来提交数据给服务器的，不管后台的服务盞用的是Django还是PHP语言还是其他语言。只要 把input标签放在form标签中，然后再添加一个提交按钮，那么以后点击提交按钮，就可以将input标签中对应的值提交给服务器 了。 Django中的表单： Django中的表单丰富了传统的HTML语言中的表单。在Django中的表单，主要做以下两件事： 1. 渲染表单模板。 2. 表单验证数据是否合法。 Django中表单使用流程： 在讲解Django表单的具体每部分的细节之前。我们首先先来看下整体的使用流程。这里以一个做一个留言板为例。首先我们在后台 服务器定义一个表单类，继承自django.forms.Form示例代码如下： 定义一个forms.py

from django import  forms
class MesssageBoardForm(forms.Form):
    title = forms.CharField(max\_length=100,min\_length=3,label='标题',error\_messages={"输入错误"})
    content = forms.CharField(widget=forms.Textarea,label='内容')  ###forms.Textarea文本框
    email = forms.EmailField(label='邮箱')
    reply = forms.BooleanField(required=False,label='是否需要回复？')   ##required是否默认勾选

定义一个views.py

from django.shortcuts import render
from django.views.generic import View
from .forms import MesssageBoardForm
class IndexView(View):
    def get(self,request):
        form = MesssageBoardForm()     ###渲染这个表单
        return render(request,'index.html',context={'form':form})
    def post(self,request):
        form = MesssageBoardForm(request.POST)
        if form.is\_valid():                   #####如果验证成功
            title = form.cleaned\_data.get('title')  ####提取验证成功的'title'
            content = form.cleaned\_data.get('content')
            email = form.cleaned\_data.get('email')
            reply = form.cleaned\_data.get('reply')
            print('\*'\*30)
            print(title,content,email,reply)
            print('\*' \* 30)
            return HttpResponse('执行成功')
        else:
            print(form.errors.get\_json\_data())   ###如果验证失败，将错误代码转换城json数据
            return HttpResponse('验证失败')

在index.html中去展示

<form action="" method="post">
    <table>
        { { form.as\_table } }
        <tr>
            <td><input type="submit" value="提交"></td>
        </tr>
    </table>
</form>

## 二、验证表单中一些常用Field

用表单验证数据 常用的Field: 使用Field可以是对数据验证的第一步。你期待这个提交上来的数据是什么类型，那么就使用什么类型的Field .   CharField： 用来接收文本。 参数： • max\_length：这个字段值的最大长度。 • min\_length：这个字段值的最小长度。 • required：这个字段是否是必须的，默认是必须的。 • error\_messages：在某个条件验证失败的时候，给出错误信息。   EmailField： 用来接收邮件，会自动验证邮件是否合法， 错误信息的key： required,invalid   FloatField： 用来接收浮点类型，并且如果验证通过后，会将这个字段的值转换为浮点类型， 参数： • max\_value：最大的值。 • min\_value：最小的值。 错误信息的key: required、invalid、max\_value、min\_value IntegerField： 用来接收整形，并且验证通过后，会将这个字段的值转换为整形。 参数： • max\_value：最大的值。 • min\_value：最小的值。 错误信息的key：required、 invalid、 max\_value、 min\_value URLField： 用来接收格式的字符串。 错误信息的key: required、invalid   常用验证器： 在验证某个字段的时候，可以传递一个validators参数用来指定捡证器，进一步对数据进行过滤。验证器有很多，但是很多验证器 我们其实已经通过这个Field或者一些参数就可以指定了。比如EmailValidator,我们可以通过EmailField来指定，比如MaxValueValidator ,我们可以通过max\_value参数来指定。以下是一些常用的验证器： 1. MaxValueValidator :验证最大值。 2. MinValueValidator :验证最小值。 3. MinLengthValidator :验证最小长度。 4. MaxLengthValidator :验证最大长度。 5. EmailValidator :验证是邮箱格式。 6. URLValidator :验证是否是URL格式。 7. Regexvalidator :如果还需要更加复杂的验证，那么我们可以通过正则表达式的验证器：RegexValidator。比如现在要验证手 机号码是否合格，那么我们可以通过以下代码实现：

from django import  forms
from django.core import validators
class MesssageBoardForm(forms.Form):
    email = forms.CharField(validators=\[validators.EmailValidator(message='请输入正确格式的邮箱！')\])

## 自定义字段验证

有时候对一个字段验证，不是一个长度，一个正则表达式能够写清楚的，还需要一些其他复杂的逻辑，那么我们可以对某个字段，进行自定义的验证。比如在注册的表单验证中，我们想要验证手机号码是否已经被注册过了，那么这时候就需要在数据库中进行判断才知道。对某个字段逬行自定义的验证方式是，定义一个方法，这个方法的名字定义规则是：clean.fieldname。如果验证失败、那么就抛出一个验证错误。比如要验证用户表中手机号码之前是否在数据库中存在，那么可以通过以下代码实现： 完整代码参考：[https://post.332b.com/post/385.html](https://post.332b.com/post/385.html)

def clean\_tel(self):
    tel = self.cleaned\_data.get('tel')  ###可以对tel字段进行二次验证,优先执行本段，然后去执行视图函数中的字段
    exists = User.objects.filter(tel=tel).exists()   ###查找是否有相同字段
    if exists:
        raise forms.ValidationError(message='tel验证失败，因为已经存在了') ###抛出异常，停止执行
    return tel

## 简化表单错误信息的提取

如果验证失败了，那么有一些错误信息是我们需要传给前端的。这时候我们可以通过以下属性来获取： 1. fom.errors :这个属性获取的错误信息是一个包含了html标签的错误信息。 2. form.errors.get\_json\_data() :这个方法获取到的是一个字典类型的错误信息。将某个字段的名字作为key，错误信息作为值的 一个字典。 3. fom.as\_json():这个方法是将form.get\_json\_data()返回的字典dump成json格式的字符串，方便进行传输。 4. 上迷方法获取的字段的错误值，都是一个比较复杂的数据。比如以下：

class Index(forms.Form):
    def get\_errors(self):
        errors = self.errors.get\_json\_data()
        new\_errors = {}
        for key,message\_dicts in errors.items():
            messages = \[\]
            for message\_dict in message\_dicts:
                message = message\_dict\['message'\]
                messages.append(message)
            new\_errors\[key\] = messages
        return new\_errors

## ModelForm

大家在写表单的时候，会发现表单中的Field和模型中的Field基本上是一模一样的，而且表单中需要验证的数据, 型中需要保存的。那么这时候我们就可以将模型中的字段和表单中的字段进行绑定。 比如现在有个Book的模型。示例代码如下：

from django.db import models
from django.core import validators
class Book(models.Model):
    title = models.CharField(max\_length=100)
    page = models.IntegerField()
    price = models.FloatField(validators=\[validators.MaxValueValidator(limit\_value=100)\])

那么在写表单的时候，就不需要把Article模型中所有的字段都一个个重复写一遍了。示例代码如下:

from django import forms
from .models import Book
class AddBookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = '\_\_all\_\_'

对出一些出错的信息，可以进行中文化处理，方便理解

    class Meta:
        model= Book
        fields = '\_\_all\_\_'
        error\_messages = {
    'page':{
        'required':'请传入page参数',
        'invalid':'请输入一个可用的page参数'
    },
    'title':{
        'max\_length':'title不能超过100字符'
    },
    'price':{
        'max\_value':'最大不能超过100元'
    }

}

### save方法：

ModelForm还有save方法，可以在验证完成后直接调用save方法，就可以将这个数据保存到数据库中了，便捷又简单直接可以省掉6行代码，示例代码如下：

def add\_book(request):
    form = AddBookForm(request.POST)
    if form.is\_valid():
        ### title = form.cleaned\_data.get('title')
        ### page = form.cleaned\_data.get('page')
        ### price = form.cleaned\_data.get('price')
        ### print('title:%s'% title)
        ### print('page:%s' % page)
        ### print('price:%s'% price)
        form.save()
        return HttpResponse('执行成功')
    else:
        print(form.errors.get\_json\_data())
        return HttpResponse('执行失败')

这个方法必须要在clean没有问题后才能使用，如果在clean之前使用、会抛出异常。另外，我们在调用save方法的时候，如果传 入一个commit=False ,那么只会生成这个模型的对象，而不会把这个对象真正的插入到数据库中。比如表单上验证的字段没有包合 模型中所有的字段，这时候就可以先创建对象，再根据填充其他字段，把所有字段的值都朴充完成后，再保存到数据库中。完整代码可以参考[https://post.332b.com/post/385.html](https://post.332b.com/post/385.html)示例代码 如下：

def reg(request):
    form = Reg(request.POST)
    if form.is\_valid():
        user = form.save(commit=False)
        user.password = form.cleaned\_data.get('pw1')
        user.save()
        return HttpResponse('注册成功')
    else:
        print(form.errors.get\_json\_data())
        return HttpResponse('注册失败')

## 文件上传

文件上传是网站开发中非常常见的功能。这里详细讲述如何在Django中实现文件的上传功能。 前端HTML代码实现： 1.在前端中，我们雷要填入一个form标签，然后在这个form标签中指定enctype="multipart/form-data" 2.在form标签中添加一个input标签，然后指定input标签的name ,以及type="file"。 以上两步的示例代码如下：

<form action="" method="post" enctype="multipart/form-data">
    <input type="file" name="myfile">
    <input type="submit" value="提交">
</form>

后端的代码实现: 后端的主要工作是接收文件。然后存储文件。接收文件的方式跟接收POST的方式是一样的，只不过是通过FILES来实现。示例代码如下：

class IndexView(View):
    def get(self,request):
        return render(request,'index.html')
    def post(self,request):
        myfile = request.FILES.get('myfile')
        with open('somefile.txt','wb') as fp:
            for chunk in myfile.chunks():
                fp.write(chunk)
        return HttpResponse('上传成功')

### 使用模型来处理上传的文件:

在定义模型的时候，我们可以给存储文件的字段指定为FileField，这个Field可以传递一个upload\_to='files'参数，用来指定上传上来的文件保存到哪里。比如我们让他保存到项目的files文件夹下，那么示例代码如下：

##models.py
from django.db import models
class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    thumbnial = models.FileField(upload\_to='files')

##views.py
class Fileindex(View):
    def get(self,request):
        return render(request,'fileindex.html')
    def post(self,request):
        title = request.POST.get('title')
        content = request.POST.get('content')
        file = request.FILES.get('myfile')
        Article.objects.create(title=title,content=content,thumbnial=file)
        return HttpResponse('执行成功')

调用完Article.objects.create方法，就会把文件保存到files下面，并且会将这个文件的路径存储到数据库中。

### 指定 MEDIA\_ROOT 和 MEDIA\_URL :

以上我们是使用了 upload\_to来指定上传的文件的目录。我们也可以指定MEDIA\_ROOT ,就不需要在FielField中指定upload\_to ,他会自动的将文件上传到MEDIA\_ROOT的目录下，下面是制定本项目的media文件的一个示例

####在setting.py中指定下面选项
MEDIA\_ROOT = os.path.join(BASE\_DIR,'media')
MEDIA\_URL = '/media/'

然后我们可以在urls.py中添加MEDIA.ROOT目录下的访问路径。示例代码如下:

from django.urls import path
from django.conf import settings
from django.conf.urls.static import static
urlpatterns = \[
\] + static(settings.MEDIA\_URL,document\_root=settings.MEDIA\_ROOT)

如果我们同时指定MEDIA\_ROOT和upload\_to ,那么会将文件上传到MEDIA\_ROOT下的upload\_to文件夹中，如果是upload\_to='%Y/%m/%d'则会保存目录，按照年月日来归类，示例代码如下:

from django.db import models
class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    thumbnial = models.FileField(upload\_to='files')

### 限制上传的文件拓展名:

如果想要限制上传的文件的拓展名，那么我们就需要用到表单来进行限制。我们可以使用普通的form表单，也可以使 用ModelForm ,直接从模型中读取字段。示例代码如下：

##models.py
from django.db import models
from django.core import validators
class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    thumbnial = models.FileField(validators=\[validators.FileExtensionValidator(\['txt','pdf'\],message=\['只能上传TXT和PDF文档'\])\])

##forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = '\_\_all\_\_'

###views.py
class Index1(View):
    def get(self,request):
        return render(request,'io.html')

    def post(self,request):
        form = ArticleForm(request.POST,request.FILES)
        if form.is\_valid():
            form.save()
            return HttpResponse('执行成功')
        else:
            print(form.errors.get\_json\_data())
            return HttpResponse('错误')

上传图片： 注意：ImageField验证图片要安装pip install Pillow 上传图片跟上传普通文件是一样的。只不过是上传图片的时候Django会判断上传的文件是否是图片的格式（除了判断后缀名，还会 判断是否是可用的图片）。如果不是，那么就会验证失败。我们首先先来定义一个包含ImageField的模型。示例代码如下：

class Article(models.Model):
    title = models.CharField(max\_length=100)
    content = models.TextField()
    thumbnial = models.ImageField()