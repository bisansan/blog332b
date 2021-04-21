---
title: 'OperationalError at /onetoone和no such table: auth_use'
tags: []
id: '431'
categories:
  - - Python
  - - 技术分享
date: 2019-01-02 11:55:58
---

CommandError: Can't find xgettext. Make sure you have GNU gettext tools 0.15 or newer installed. 下载： http://gnuwin32.sourceforge.net/packages/gettext.htm 配置环境变量 C:\\Program Files (x86)\\GnuWin32\\bin 输出以下结果，就ok了，记得重启命令行 C:\\Users\\admin>xgettext xgettext: no input file given Try \`(null) --help' for more information. django会爆出这样的错误，我检查了代码并没有发现什么问题，最后发现是因为没有进行数据库映射导致的，makemigrations和migrate操作一下 Not Found: / \[02/Jan/2019 11:35:42\] "GET / HTTP/1.1" 404 2032 Internal Server Error: /onetoone Traceback (most recent call last): sqlite3.OperationalError: no such table: auth\_user The above exception was the direct cause of the following exception: django.db.utils.OperationalError: no such table: auth\_user  

Request Method:

GET

Request URL:

http://127.0.0.1:8000/onetoone

Django Version:

2.1.4

Exception Type:

OperationalError

Exception Value:

no such table: auth\_user

Exception Location:

C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\lib\\site-packages\\django\\db\\backends\\sqlite3\\base.py in execute, line 296

Python Executable:

C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe

Python Version:

3.7.1

Python Path:

\['C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled1',
 'C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled1',
 'C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled\\\\venv\\\\Scripts\\\\python37.zip',
 'C:\\\\Users\\\\Administrator\\\\AppData\\\\Local\\\\Programs\\\\Python\\\\Python37\\\\DLLs',
 'C:\\\\Users\\\\Administrator\\\\AppData\\\\Local\\\\Programs\\\\Python\\\\Python37\\\\lib',
 'C:\\\\Users\\\\Administrator\\\\AppData\\\\Local\\\\Programs\\\\Python\\\\Python37',
 'C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled\\\\venv',
 'C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled\\\\venv\\\\lib\\\\site-packages',
 'C:\\\\Users\\\\Administrator\\\\PycharmProjects\\\\untitled\\\\venv\\\\lib\\\\site-packages\\\\setuptools-39.1.0-py3.7.egg',
 'C:\\\\Program Files\\\\JetBrains\\\\PyCharm '
 '2018.1.4\\\\helpers\\\\pycharm\_matplotlib\_backend'\]

Server time:

Wed, 2 Jan 2019 03:35:56 +0000

## Traceback [Switch to copy-and-paste view](http://127.0.0.1:8000/onetoone#)

*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `_execute`
    
    85.                  return self.cursor.execute(sql, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\sqlite3\base.py` in `execute`
    
    296.          return Database.Cursor.execute(self, query, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   ### The above exception (no such table: auth\_user) was the direct cause of the following exception:
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\core\handlers\exception.py` in `inner`
    
    34.              response = get\_response(request)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\core\handlers\base.py` in `_get_response`
    
    126.                  response = self.process\_exception\_by\_middleware(e, request)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\core\handlers\base.py` in `_get_response`
    
    124.                  response = wrapped\_callback(request, \*callback\_args, \*\*callback\_kwargs)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled1\front\views.py` in `one_view`
    
    8.      user = User.objects.create(username='zhiliao1',email='2115445@qq.com')
        
        ...
    
    [▼ Local vars](http://127.0.0.1:8000/onetoone#)
    
    Variable
    
    Value
    
    request
    
    <WSGIRequest: GET '/onetoone'>
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\manager.py` in `manager_method`
    
    82.                  return getattr(self.get\_queryset(), name)(\*args, \*\*kwargs)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\query.py` in `create`
    
    413.          obj.save(force\_insert=True, using=self.db)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\contrib\auth\base_user.py` in `save`
    
    73.          super().save(\*args, \*\*kwargs)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\base.py` in `save`
    
    718.                         force\_update=force\_update, update\_fields=update\_fields)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\base.py` in `save_base`
    
    748.              updated = self.\_save\_table(raw, cls, force\_insert, force\_update, using, update\_fields)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\base.py` in `_save_table`
    
    831.              result = self.\_do\_insert(cls.\_base\_manager, using, fields, update\_pk, raw)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\base.py` in `_do_insert`
    
    869.                                 using=using, raw=raw)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\manager.py` in `manager_method`
    
    82.                  return getattr(self.get\_queryset(), name)(\*args, \*\*kwargs)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\query.py` in `_insert`
    
    1136.          return query.get\_compiler(using=using).execute\_sql(return\_id)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\models\sql\compiler.py` in `execute_sql`
    
    1289.                  cursor.execute(sql, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `execute`
    
    100.              return super().execute(sql, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `execute`
    
    68.          return self.\_execute\_with\_wrappers(sql, params, many=False, executor=self.\_execute)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `_execute_with_wrappers`
    
    77.          return executor(sql, params, many, context)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `_execute`
    
    85.                  return self.cursor.execute(sql, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\utils.py` in `__exit__`
    
    89.                  raise dj\_exc\_value.with\_traceback(traceback) from exc\_value
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\utils.py` in `_execute`
    
    85.                  return self.cursor.execute(sql, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)
    
*   `C:\Users\Administrator\PycharmProjects\untitled\venv\lib\site-packages\django\db\backends\sqlite3\base.py` in `execute`
    
    296.          return Database.Cursor.execute(self, query, params)
        
        ...
    
    [▶ Local vars](http://127.0.0.1:8000/onetoone#)