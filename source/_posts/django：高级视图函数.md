---
title: Django：高级视图函数
tags: []
id: '671'
categories:
  - - Django
date: 2018-11-30 15:37:49
---

### 一、method限制提交提交请求的类型

限制提交请求的模块在django.views.decorators.http，它们分别是

1.  require\_http\_methods限制单种或多种请求
2.  require\_GET：只允许GET请求
3.  require\_POST：只允许POST请求

from django.views.decorators.http import require\_http\_methods,require\_GET,require\_POST

在视图函数请的使用方法，就是像使用装饰器一样

####@require\_http\_methods(\['GET','POST'\])   可以同时允许多种请求
@require\_GET
def index(request):
    front = Front.objects.all()
    return render(request,'index.html',context={"front":front})

在一个视图函数中根据不同的请求来执行命令方法

def add\_article(request):
    if request.method == 'GET':
        return render(request,'add.html')
    else:
        title = request.POST.get("title")
        content = request.POST.get("content")
        Front.objects.create(title=title, content=content)
        return HttpResponse('添加成功')

### 二、重定向和页面跳转

重定向分为301永久性重定向和302暂时性重定向，重定向的模块在django.shortcuts模块中

1.  redirect可以设置你要跳转的URL，这个是302暂时性重定向
2.  reverse是反转和引用项目urls.py中，已经设置了name属性的网址

from django.shortcuts import redirect,reverse

在视图函数中是使用方法如下

def index(request):
    return redirect(reverse('add'))      引用反转URL
   #return redirect('https://post.332b.com/')   直接写死URL

### 三、WSGIRequest对象

1.path：请求网址的路径，get\_full\_path：会带有查询查询参数的full，get\_raw\_uri：是完整的URL，get\_host：域名加上端口号 例如https://blog.csdn.net/goodfav/?id=1111

1.  path：/goodfav/
2.  get\_full\_path：/goodfav/?id=1111
3.  get\_raw\_uri：https://blog.csdn.net/goodfav/?id=1111
4.  get\_host：blog.csdn.net:443

def index(request):
    print(request.get\_raw\_uri())
    return HttpResponse('首页')

2.method：获取当前的请求类型，用法参照（一） 3.GET：QueruDict对象，包含查询字符串，以字典的形式获取，例如https://blog.csdn.net/?id=1111后面的id=1111 4.POST：QueruDict对象，包含所有以POST上传的数据 5.FILES：QueruDict对象，包含所有的上传文件 6.COOKIES：一个标准的字典类型，包含所有的cookies，键值对都是字符串类型 7.session：一个类似字典的对象，用来操作服务器上的session 8.META：存储客户端发送的所有header信息 推荐META判断IP方式如下

def index(request):
    if request.META.has\_key('HTTP\_X\_FORWARDED\_FOR'):
        ip = request.META\['HTTP\_X\_FORWARDED\_FOR'\]
    else:
        ip = request.META\['REMOTE\_ADDR'\]

is\_secure()：布尔类型，判断当前请求是否是https is\_ajax()：布尔类型，根据请求头是否有X-Request-With:XMLHttpRequest来判断是否采用的ajax请求

### QueryDict对象

request.GET和request.POST都是QueryDict对象，它有两种用法，一种是get方法，另外一种是getlist方法 1.get：用来获取key的值，如果没有key则会返回None 2.getlist：如果浏览器上传一个key的对个值，同过这个方法获取就会返回一个列表

### HttpResponse 对象

Django服务器接收到客户端发送过来的请求后，会将提交上来的这些数据封装成一个HttpRequest对象传给视图函数。那么视图函数在处理完相关的逻辑后，也需要返回一个响应给浏览器。而这个响应，我们必須返回HttpResponseBase或者他的子类的对象。而HttpResponse则是HttpResponseBase用得最多的子类。那么接下来就来介绍一下HttpResponse及其子类。

#### 常用属性：

1\. content:返回的内容。 2. status\_code:返回的HTTP响应状态码。 3. content.type:返回的数据的MIME类型，默认为text/html ◊湖贫器会根据这个属性，来显示数据。如果是text/html，那么 就会解析这个字符串，如果text/plain ,那么就会显示一个纯文本。常用的Content-Type如下：

1.  text/html (默认的，html文件）
2.  text/plain (纯文本）
3.  text/css (css文件〉
4.  text/javascript (js文件）
5.  multipart/form-data (文件提交）
6.  application/json (json传输)
7.  application/xml (xml文件）

4 .设置请求头：response\['X-Acccss-Token'\] = ’xxxx'。

#### 常用方法:

1.set\_cookie：用来设置cookie信息，后面讲到授权的时候会看重讲到。 2.delete\_cookie：用来删除 cookie 信息。 3.write： HttpResponse是一个类似于文件的对象（content属性，也就是直接在网页这个插入内容）

def index(request):
    response = HttpResponse('我是文字',content\_type='text/plain;charset=utf-8')   ###将文本设置成UTF-8编码
    response.status\_code = 400     ####状态码为400
    response.write('，后加入文字')
    return response

### JsonResponse 对象

将字典对象dumps成字符串，通过HttpResponse传给浏览器

def index(request):
    person = {
        'username':'pingguo',
        'age':18,
        'height':180
    }
    ######person\_str = json.dumps(person)      ###import json
    #####response = HttpResponse(person\_str,content\_type='application/json')
    response = JsonResponse(person)      ###这一行等于上面两行
    return response

如果对象是一个列表的话，就只能这样的传

def index(request):   
    persons = \['知了','苹果','香蕉'\]
    response = JsonResponse(persons,safe=False)
    return response

这里再来对每个部分的代码进行解释： 1 •我们在初始化HttpResponse的时候,指定了Content-Type为text/csv,这将告诉浏览器，这是一个csv格式的文件而不是一 个HTML格式的文件，如果用默认值，默认值就是html，那么浏览器将把csv格式的文件按照html格式输出,这肯定不是我们想要的。 2. 第二个我们还在response中添加一个Content-Disposition头，这个东西是用来告诉浏览器该如何处理这个文件，我们给这个头 的值设罝为attachment;,那么浏览器将不会对这个文件进行显示，而是作为附件的形式下载，第二 个filename=Msomefilename.csv"是用来指定这个csv文件的名字。 3. 我们使用csv模快的writer方法，将相应的数据写入到response中。

### CSV文件下载和大型CSV文件处理

定义一个普通的csv文件下载，通过python内置CSV模块来实现

def index(request):
    response = HttpResponse(content\_type='text/csv')
    response\['Content-Disposition'\] = "attachment;filename='abc.csv'"     ###处理这个Content，作为附件下载并且文件名为abc.csv
    # with open('xx.csv','w') as fp:
    #     csv.writer(fp)
    write = csv.writer(response)   ##这个等于上面两行代码
    write.writerow(\['username','简单'\])
    write.writerow(\['age',18\])
    return response

定义一个普通的csv文件下载，通过Django模板来实现

from django.template import loader,Context
def reindex(request):
    response = HttpResponse(content\_type='text/csv')
    response\['Content-Disposition'\] = "attachment;filename='abc.csv'"
    context = {
        'row':\[
            \['username','witt'\],
            \['age',18\],
        \]
    }
    template = loader.get\_template('abc.txt')    ###获取一下abc.txt模板
    csv\_template = template.render(context=context)
    response.content = csv\_template
    return response

template目录下的abc.txt代码，如果反复出现空行和文字交错，请将{ { row.0 } },{ { row.1 } }放在首行

{ % for row in rows %}
{ { row.0 } },{ { row.1 } }
{ % endfor %}

### 关于StreamingHttpResponse

这个类是专门用来处理流数据的。使得在处理一些大型文件的时候，不会因为服务器处理时间过长而到时连接超时。这个类不是继承 自HttpResponse，并且跟HttpResponse对比有以下几点区别： 1•这个类没有属性content ,相反是streaming\_content。 2. 这个类的streaming\_content必须是一个可以迭代的对象。 3. 这个类没有write方法，如果给这个类的对象写入数据将会报错， 注意：StreamingHttpResponse会启动一个进程来和客户端保持长连接，所以会很消耗资源口所以如果不是特殊要求，尽量少用这种 方法。 下面就是标准的示范

def relindex(request):
    response = StreamingHttpResponse(content\_type='text/csv')
    response\['Content-Disposition'\] = "attachment;filename='big.csv'"
    rows = ("Row {},{}\\n".format(row,row) for row in range(0,100000000))
    #response.streaming\_content = ('username,age\\n','zhiliao,18')
    response.streaming\_content = rows
    return response

这个就是一个相反的结果，等待时间长

def relindex(request):
    response = HttpResponse(content\_type='text/csv')
    response\['Content-Disposition'\] = "attachment;filename='big.csv'"
    writer = csv.writer(response)      ####这里调用了csv模块就变慢了
    for row in range(0,10000000):
        writer.writerow(\['Row {}'.format(row),'{}'.format(row)\])
    #####无用代码response.streaming\_content = ('username,age\\n','zhiliao,18')
    #####无用代码response.streaming\_content = rows
    return response

下面就是一个 View django.views.generic.base.View是主要的类视图，所有的类视图都是继承自他，如果我们写自己的类视图，也可以继承自他。然后再根据当前请求method ,来实现不同的方法。比如这个视图只能使用get的方式来请求，那么就可以在这个类中定义get(self,request,\*args,\*\*kwargs)方法。以此类推，如果只需要实现post方法，那么就只需要在类中实 现 post(self, equest,\*args,\*\*kwargs)

from django.views.generic import View
class BookListView(View):
    def get(self,request,\*args,\*\*kwargs):
        return HttpResponse('book list')

在URL中要这样设置，要通过as\_view()来转换

urlpatterns = \[
    path('book/',BookListView.as\_view())
\]

除了 get 方法，View 还支持以下方法\['get','post','put','patch','delete','head','options','trace'\] 如果用户访问了View中没有定义的方法。比如你的类视图只支持get方法，而出现了 post方法，那么就会把这个请求转发 给 http\_raethod\_not\_allowed(request,\*args,\*\*kwargs)示例代碎如下：

from django.views.generic import View
class BookListView(View):
    def get(self,request,\*args,\*\*kwargs):
        return HttpResponse('book list')
    def http\_method\_not\_allowed(self, request, \*args, \*\*kwargs):
        return HttpResponse('不支持其他请求')

不管是post还是get请求，或者是404错误等等都会走dispatch(request, \*args, \*\*kwargs)

from django.views.generic import View
class BookListView(View):
    def get(self,request,\*args,\*\*kwargs):
        return HttpResponse('book list')
    def dispatch(self, request, \*args, \*\*kwargs):
        print("你好")
        return super(BookListView,self).dispatch(request,\*args, \*\*kwargs)
    def http\_method\_not\_allowed(self, request, \*args, \*\*kwargs):
        return HttpResponse('不支持其他请求')

TemplateView模板 用来映射静态模板，一般都比较推荐使用这个，两行代码就可以搞定一个静态模板映射，template\_name指定静态模板路径

from django.views.generic import TemplateView
path('', TemplateView.as\_view(template\_name='about.html')),

他有一个上下文参数，get\_context\_data

from django.views.generic import View,TemplateView
class About(TemplateView):
    template\_name = 'about.html'
    def get\_context\_data(self, \*\*kwargs):
        content= {
            'hp':'078312345678'
        }
        return content
urlpatterns = \[
    path('', About.as\_view()),
\]

然后在模板about.html中动态显示

<body>
这个是主页{ { hp } }
</body>

### Paginator 和 Page 类：

Paginator和Page类都是用来做分页的。他们在Django中的路径 为django.core.paginator.Paginator和django.core.paginator.Page,以下对这两个类的末用厲性和方法做解释： Paginator常用方法和方法: 1. count :总共有多少条数据。 2. num\_pages :总共有多少页 3. page.range :页面的区间。比如有三页，那么就range(1,4) Page常用属性和方法： 1 has\_next :是否还有下一页。 2. has\_previous :是否还有上一页。 3. next\_page\_number :下一页的页码。 4. previous\_page\_number :上—页的页码 5. number :当前页。 6. start\_index :当前这一页的第一条鈐据的索引值。 7. end\_index :当前这一页的最后一条数据的索引值。

class ArticleListView(ListView):
    model = Article    ###对应的模块
    template\_name = 'list.html'    ####对应的模板
    paginate\_by = 10        ###没页显示数量
    context\_object\_name = 'articles'   ####展示在模板中的变量名字
    ordering = 'create\_time'    ###排序规则
    page\_kwarg = 'p'       ####翻页参数名称,不设置的话就是page

    def get\_context\_data(self, \*\*kwargs):
        context = super(ArticleListView, self).get\_context\_data(\*\*kwargs)
        # context\['username'\] = 'apple'
        paginator = context.get('paginator')   ###获取pagintor属性
        page\_obj = context.get('page\_obj')
        print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*'\*3)
        print(paginator.count)      ####获取数据数量
        print(paginator.num\_pages)   ####获取数据页数
        print(paginator.page\_range)  ####获取页数的区间，例如range(1,22)
        print(page\_obj.has\_next())    ####判断是否有下一页
        print(page\_obj.has\_previous())    ####判断是否有上一页
        print(page\_obj.next\_page\_number())   ####返回下一页的页码，如果没有值，会报错
        print(page\_obj.previous\_page\_number())   ####返回上一页的页码，同上
        print(page\_obj.number)     ####获取当前页码
        print(page\_obj.start\_index())    ####返回当前页的第一个索引值
        print(page\_obj.end\_index())   ####返回当前页的最后一个索引值
        print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*'\*3)
        return context
    #def get\_queryset(self):
        #return Article.objects.filter(id\_\_lte=9)   ####过滤文章

在模板list.html中显示

{ % for foo in articles %}
<li>{ { foo.title } }</li>
{ % endfor %}

一个分页算法的实例

from django.shortcuts import render
from .models import Article
from django.http import HttpResponse
from django.views.generic import ListView

def add\_artilcle(request):
    articles = \[\]
    for x in range(0,102):
        article = Article(title='标题：%s'%x,content='内容：%s'%x)
        articles.append(article)
    Article.objects.bulk\_create(articles)
    return HttpResponse('执行成功')

class ArticleListView(ListView):
    model = Article    ###对应的模块
    template\_name = 'html2.html'    ####对应的模板
    paginate\_by = 10        ###没页显示数量
    context\_object\_name = 'articles'   ####展示在模板中的变量名字
    ordering = 'create\_time'    ###排序规则
    page\_kwarg = 'p'       ####翻页参数名称,不设置的话就是page

    def get\_context\_data(self, \*\*kwargs):
        context = super(ArticleListView, self).get\_context\_data(\*\*kwargs)
        # context\['username'\] = 'apple'
        paginator = context.get('paginator')   ###获取pagintor属性
        page\_obj = context.get('page\_obj')
        #print(context)
        pagination\_data = self.get\_paginator\_data(paginator,page\_obj)
        context.update(pagination\_data)       ####将get\_paginator\_data添加到context
        # print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*'\*3)
        # print(paginator.count)      ####获取数据数量
        # print(paginator.num\_pages)   ####获取数据页数
        # print(paginator.page\_range)  ####获取页数的区间，例如range(1,22)
        # print(page\_obj.has\_next())    ####判断是否有下一页
        # print(page\_obj.has\_previous())    ####判断是否有上一页
        # print(page\_obj.next\_page\_number())   ####返回下一页的页码，如果没有值，会报错
        # print(page\_obj.previous\_page\_number())   ####返回上一页的页码，同上
        # print(page\_obj.number)     ####获取当前页码
        # print(page\_obj.start\_index())    ####返回当前页的第一个索引值
        # print(page\_obj.end\_index())   ####返回当前页的最后一个索引值
        # print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*'\*3)
        return context
    def get\_paginator\_data(self,paginator,page\_obj,around\_count=2):
        current\_page = page\_obj.number
        sum\_pages = paginator.num\_pages
        print(sum\_pages)
        left\_pages\_start = False
        right\_pages\_end= False
        if current\_page <= around\_count+1:
            left\_pages = range(1,current\_page)
        else:
            left\_pages\_start = True
            left\_pages = range(current\_page-around\_count, current\_page)
            #print(left\_pages)
        if sum\_pages - current\_page >= around\_count:
            right\_pages\_end = True
            right\_pages = range(current\_page+1,current\_page+around\_count+1)
        else:
            right\_pages = range(current\_page+1,sum\_pages+1)
        # if current\_page >= sum\_pages - around\_count - 1:
        #     right\_pages = range(current\_page+1,sum\_pages+1)
        #     print(right\_pages)
        # else:
        #     right\_pages = range(current\_page+1,current\_page+around\_count+1)
        print(right\_pages)
        return {
            'left\_pages':left\_pages,
            'right\_pages':right\_pages,
            'current\_page':current\_page,
            'left\_pages\_start':left\_pages\_start,
            'right\_pages\_end':right\_pages\_end
        }
    #def get\_queryset(self):
        #return Article.objects.filter(id\_\_lte=9)   ####过滤文章
# Create your views here.

分页算法在模板中的应用

<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
</head>
<body>
<ul>
{ {    展示文章} }
    { % for article in articles %}
        <li>{ { article.content } }</li>
    { % endfor %}
    <ul class="pagination">
{ {        上一页} }
        { % if page\_obj.has\_previous %}
            <li><a href="{ % url 'index' %}?p={ { page\_obj.previous\_page\_number } }">上一页</a></li>
        { % else %}
            <li class="disabled"><a href="#">上一页</a></li>
        { % endif %}
{ {        返回第一页} }
        { % if left\_pages\_start %}
            <li><a href="{ % url 'index' %}?p=1">1</a></li>
            <li><a href="javascript:void(0);">...</a></li>
        { % endif %}
{ {        左边页码} }
        { % for left\_page in left\_pages %}
            <li><a href="{ % url 'index' %}?p={ { left\_page } }">{ { left\_page } }</a></li>
        { % endfor %}
{ {        中间页码} }
        <li class="active"><a href="{ % url 'index' %}?p={ { current\_page } }">{ { current\_page } }</a></li>
{ {        右边页码} }
            { % for right\_page in right\_pages %}
                <li><a href="{ % url 'index' %}?p={ { right\_page } }">{ { right\_page } }</a></li>
            { % endfor %}
{ {        返回最后一页} }
        { % if right\_pages\_end %}
            <li><a href="javascript:void(0);">...</a></li>
            <li><a href="{ % url 'index' %}?p={ { paginator.num\_pages } }">{ { paginator.num\_pages } }</a></li>
        { % endif %}
{ {        下一页} }
        { % if page\_obj.has\_next %}
            <li><a href="{ % url 'index' %}?p={ { page\_obj.next\_page\_number } }">下一页</a></li>
        { % else %}
            <li class="disabled"><a href="#">下一页</a></li>
        { % endif %}
    </ul>
</ul>
</body>
</html>

给类视图添加装饰器

from django.http import HttpResponse
from django.views import View
from django.utils.decorators import method\_decorator
def login\_required(func):
    def wrapper(request,\*args,\*\*kwargs):
        username = request.GET.get('username')
        if username:
            return func(request,\*args,\*\*kwargs)
        else:
            return redirect(reverse('login'))
    return wrapper

@method\_decorator(login\_required,name='dispatch')
class ProfileView(View):
    def get(self,request):
        return HttpResponse('用户界面')
def login(request):
    return HttpResponse("登陆页面")

状态码错误处理 • 404 :服务器没有指定的Ud。 • 403 :没有权限访问相关的数据。 • 405 :请求的method错误。 • 400 : bad request ,请求的参数错误。 • 500 :服务器内部错误，一般是代码出bug了。 • 502 : 一般部署的时候见得比较多，一般是nginx启幼了，然后uwsgi有问题。 自定义错误模板： 在碰到比如404 , 500错误的时候，想要返回自己定义的模板。那么可以直接在templates文件夹下创建相应错误代码的html摸板文件。那么以后在发生相应错误后，会将指定的模板返回回去。 -----templates --404.html --403.html 错误处理的解决方案： 对于404和500这种自动抛出的错误。我们可以直接在templates文件夹下新建相应错误代码的模板文件。而对于其他的错误，我们可以专门定义一个APP，用来处理这些错误。