---
title: Django：cookie 和session
tags: [django,python]
id: '403'
categories:
  - - 计算机编程
abbrlink: 292a9e36
date: 2018-12-18 17:54:42
---

## cookie的简介

1\. cookie：在网站中，http请求是无状态的。也就是说即使第一次和服务器连接后并且登录成功后，第二次请求服务器依然不能知 道当前请求是哪个用户。cookie的出现就是为了解决这个问题，第一次登录后服务器返回一些数据(cookie)给浏览器，然后 浏览器保存在本地，当该用户发送第二次请求的时候，就会自动的把上次请求存储的cookie数据自动的携带给服务器，服务器 通过浏览器携带的数据就能判断当前用户是哪个了，cookie存储的数据量有限，不同的浏览器有不同的存储大小，但一般不超 过4KB。因此使用cookie只能存储一些小量的数据。 2. session: session和cookie的作用有点类似，都是为了存储用户相关的信息。不同的是，cookie是存储在本地浏览 器，session是一个思路、一个概念、一个服务器存储授权信息的解决方案，不同的服务器，不同的棍架，不同的语言有不同的 实现。虽然实现不一样，但是他们的目的都是服务器为了方便存储数据的。session的出现，是为了解决cookie存储数据不安 全的问题的。 3. cookie和session结合使用：web开发发展至今，cookie和session的使用已经出现了一些非常成熟的方案。在如今的市场或 者企业里，一般有两种存储方式： 存储在服务端：通过cookie存储一个sessionid，然后具体的数据则是保存在session中。如果用户已经登录，则服务器 会在cookie中保存一个sessionid，下次再次请求的时候，会把该sessionid携带上来，服务器根 据sessionid在session库中获取用户的session数据。就能知道该用户到底是谁，以及之前保存的一些状态信息◊这种 专业术语叫做server side session，Django把session信息默认存储到数据痒中，当然也可以存储到其他地方，比如缓 存中，文件系统中等。存储在服务器的数据会更加的安全，不容易被窃职。但存储在服务器也有一定的弊端，就是会占用服 务器的资源，但现在服务器已经发展至今，一些session信息还是绰绰有余的。 将session数据加密，然后存储在cookie中。这种专业术语叫做client side session

## 在 django 中操作cookie 和session:

操作cookie: 设cookie是设置给浏览器的。因此我们需要通过response的对象来设置cookie可以通过response.set\_cookie来设置,这个方法的相关参数如下： 设置cookie是设S值给浏览器的。因此我们需要通过response的对象来设设S cookie可以通过response.set\_cookie来设 S,这个方法的相关参数如下： 1. key :这个 cookie 的 key 2. value :这个 cookie 的 value 3. max\_age :最长的生命周期。单位是秒。 4. expires :过期时间。跟max\_age是类似的，只不过这个参数需要传递一个具体的日期，比如datetime或者是符合日期格式的字 符串，如果设置了 max\_age ,那么这个参数设置将无效。 5. path :对域名下哪个路径有效。默认是对域名下所有路径都有效。 6. domain :针对哪个域名有效。 7. secure :是否是安全的，如果设置为True，那么只能在https协议下才可用 8. httponly :默认是False 如果为True，那么在客户端不能通过javascript进行操作。 给cookies设置一个有效时间

def index(request):
    reponse = HttpResponse('index')
    expires = datetime(year=2018,month=12,day=30,hour=8)
    expires = make\_aware(expires)
    reponse.set\_cookie('username','zhiliao',expires=expiresmax\_age)#当存在max\_age（cookies剩余有效时间）时，优先调用expires
    return reponse

删除和清空一个cookies的值

reponse.delete\_cookie('username')

在其他网址调用cookies

def gete(request):
    cookies = request.COOKIES
    username = cookies.get('username')
    return HttpResponse(username)

给cookies设置一个指定路径，这个cookies只会对www.xxx.com/cms/xxx有效

reponse.set\_cookie('username','zhiliao',expires=expires,path='/cms/')

操作session: django中的session默认情况下是存储在服务器的数据库中的，在表中会根据sessionid来提取指定的session数据，然后再把这 个sessionid放到cookie中发送给浏览器存槠，浏览器下次在向服务器发送请求的时候会自动的把所有cookie信息都发送给服务 器，服务器再从cookie中获职sessionid，然后再从数据库中获取session数据。但是我们在操作session的时候，这些细节压根 就不用管。我们只需要通过request.session即可操作，示例代码如下： session常用的方法如下： 1. get :用来从session中获取指定值。 2. pop :从session中删除一个值。 3. keys :从session中获取所有的键。 4. items :从session中获取所有的值。 5. clear :清除当前这个用户的session数据。 6. flush :删除session并且删除在浏览器中存储的session\_id，一般在注销的时候用得比较多 7. set\_expiry(value)  :  设置session过期时间。

*   整形：代表秒数，表示多少秒后过期。
*   0  :  代表只要浏览器关闭，session就会过期。
*   None :会使用全局的session配晋,在settings.py中可以设置SESSION\_COOKIE\_AGE来配贾全局的过朗时间。默认是1209600秒，也就是2周的时间。

8\. clear\_expired :清除过期的session Django并不会清除过期的session，需要定期手动的清理，或者是在终端，使用命令 行 python manage.py clearsessions 来清除过期的 session

## 修改Session的存储机制

默认情况下，session数据是存储到数据库中的。当然也可以将session数据存储到其他地方。可以通过设罝SESSION\_ENGINE来更 改session的存储位罝，这个可以配置为以下几种方案： 1. django.contrib.sessions.backends.db :使用数据库。默认就是这种方案。 2. django.contrib.sessions.backends.file :使用文件来存储session。 3. django.contrib.sessions.backends.cache :使用缓存来存储session。想要将数据存储到缓存中，前提是你必须要在settings.py中配置好CACHES ,并且是需要使用Memcached ,而不能使用纯内存作为缓存。 4. django.contrib.sessions.backends.cached\_db :在存储数据的时候，会将数据先存到缓存中，再存到数据库中。这样就可以保证 万一缓存系统出现问题，session数据也不会丢失。在获职数据的时候，会先从缓存中获职，如果缓存中没有，那么就会从数据库中获 取。 5. django.contrib.sessions.backends.signed\_cookies :将session信息加密后存储到浏览器的cookie中。这种方式要注意安全， 建议设置SESSION\_COOKIE\_HTTPONLY=True，那么在浏览器中不能通过js来操作session数据，并且还需要对settings.py中 的SECRET\_KEY进行保密，因为一旦别人知道这个SECRET\_KEY ,那么就可以进行解密。另外还有就是在cookie中，存储的数据不能 超过4k 在setting.py中设置，如果要使用cached要配置好\[CACHES\]，参考[https://post.332b.com/post/398.html](https://post.332b.com/post/398.html)

SESSION\_ENGINE = 'django.contrib.sessions.backends.cached\_db'