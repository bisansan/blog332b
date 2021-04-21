---
title: Django数据库filter的条件查询Field查找
tags: []
id: '288'
categories:
  - - Django
abbrlink: 61cb5a6a
date: 2018-11-16 17:48:07
---

查询数据库的方式一般是filter、exclude和get方法来查询 查询条件 但是"query"只能用在“QuerySet”对象上，不能用在普通的ORM模型上，如果你是用get来查询数据，它就返回的是一个普通的ORM模型，而不是一个“QuerySet”对象，你要是通过filter等等query对象的语法来查询的，就是“QuerySet”对象

def index(request):
    article = Artile.objects.filter(id\_\_exact=1)
    ###在windows操作系统下的mysql,排序规则无论大小写都是不敏感的，但是在Linux就会区分大小写
    ###article = Artile.objects.filter(id\_\_exact=None)
    ###如果我们将这个参数设为None，mysql执行原生语句的时候就会翻译为NULL
    print(article.query) ##打印执行的原生SQL语句
    #< QuerySet\[ < Artile: Artile object(1) >\] >
    #Like和=大部分情况下是等价的
    #exict和iexactde的区别就是=和Like的区别
    return HttpResponse("str(article)")

##### icontains和contains

contains：使用大小写敏感的判断来查询数据，icontains：忽略大小写敏感的判断来查询数据,他们两个都是模糊查找（匹配查找），也就是包含所查找的值想等才符合条件

##### exict和iexactde的区别

就是=和Like的区别，他们两个所对应的是精确查询，也就是必须所查找的值想等才符合条件 提取那些给定的field的值是否在给定的容器中。容器可以为list、tuple或者任何一个可以迭代的对象，包括QuerySet对象。 示例代码如下： `articles = Article.objects.filter(id_in=[l,2,3])`

class Article(models.Model):
    title = models.CharField(max\_length=200) 
    content = models.TextField()
    cateogry models.ForeignKey( Category,on\_delete=models.CASCADE,null= True,related\_query\_name='articles')
        class Meta:
            db table = 'article'

因为在'cateogry' 的' ForeignKey' 中指定了' related\_query\_name'为'articles' ,因此你不能再使用'article'来进行反向査询了,这时候就需要通过' articles\_id\_in'来进行反向查询。 并且，如果在做反向查询的时候，如果查询的字段就是模型的主键，那么可以省略掉 这个字段，直接写成'article\_in'就可以了，不需要这个了。 'in'不仅仅可以指定列表/元组，还可以为'QuerySet' 。比如要查询“文章标题中包含有hello的所有分类”，那么可以通过以下代码来实现: `python--` `articles = Article.objects.filter(title_icontains="hello" )` `categories = Category.objects.filter(articles_in=articles)` `for cateogry in categories:` `    print(cateogry)` `......`

##### gt：

某个field的值要大于给定的值。示例代码如下: `articles = Article.objects.filte(id_gt=4)` 以上代码的意思是将所有id大于4的文意全部都找出来。 将翻译成以下SQL语句： select …where id > 4;

##### gte：

类似于et，是大于等于。

##### lt：

类似于是小于。

##### lte： 类似于lt ,是小于等于。

##### startswith：

判断某个字段的值是否是以某个值开始的。大小写敏感。示例代码如下: articles = Article.objects.filter(title\_startswith='hello') 以上代码的意思是提取所有标题以hello字符串开头的值。 将翻译成以下SQL语句： select ... where title like •hello%\*

##### istartswith：

类似于startswith ,但是大小写是不敏感的。

##### endswith：

判断某个字段的是否以某个值结束并且大小写敏感。它的用法和startswith相反，是查找以某个值结束的语句

##### iendswith：

用法同endswith，大小写不敏感

##### range：

判断某个field是否在给定的区间，也就是查找日期和日期之间的所有文章，在制定时间的时候要把给时间制定时区，不能让它变成一个幼稚时间，不然django会警告

from django.utils.timezone import make\_aware
from datetime import datetime
    start\_date = make\_aware(datetime(year«2018,month=1,day=1))
    end\_date = make\_aware(datetime(year=2018,Jmonth=3,day=29,hour=16))
    articles = Article.objects.filter(pub\_date\_range=(start\_date,end\_date))

##### data:

查找某一天所有发表值，例如要查寻某天所有的文章

articles = Article.objects.filter(pub\_date\_data=data(2018,3,28))

##### year和day

根据年或者某一天进行查找

##### week\_day

按照星期几来进行查找，1表示周日，2-6表示周一到周五，7表示周六

##### time:

根据时间进行查找，示例代码： `from django.utils.timezone import make_aware` `articles = Article.objects.filter(pub_date_time=make_aware(datetime.tim(12.12.12)))` 雷要注意的是，以上提取数据，不会包合最后一个值。也就是不会包合2018/12/12的文童。 而且另外一个重点，因为我们在settings.py中指定了 USE\_TZ=True ,并且设值了 TIME.ZONE='Asia/Shanghai',因此我们在提取数 据的时候要使用 django.utils.timezone.make\_aware 先将 datetime从 navie 时间转换为 aware 时间。make\_aware 会将指定的时间转换为time.zone中指定的时区的时间 下面代码在查找时间对象的时候为空的解决办法，因为它在查找时间对象的时候，会执行sql语句时区转换命令，但是默认mysql不带有时区文件，要去官方下载 `def index7(request):` `     articles =Article.objects.filter(create_time_date=datetime(year=2018,month=4,day=4))` 注意，因为默认情况下MySQL的表中是没有存储时区相关的信息的。因此我们需要下载一些时区区表的文件，然后添加到Mysql的配路径中。 如果你用的是 windows操作系统。那么在 http://dev.mysql.com/downloads/timezones.html 下载timezone\_2018d\_posix.zip - POSIX standard。然后将下载下来的所有文件拷到 C:\\ProgramData\\MySQL\\MySQL Server 5.7\\Data\\MySql中，如果提示文件名重复，那么选择覆盖即可◊ 如果用的是linux或者mac系统，那么在命令行中执行以下命令：mysql\_tzinfo\_to\_sql /usr/share/zoneinfo mysql -D mysql -u root -p ,然后输入密码，从系统中加载时区文件更新到mysql中。

##### isnull：

True提取所有不为空的值，False提取所有为空的值

##### regex和iregex

可以按照正则表达式的值来提取值       豆腐干豆腐