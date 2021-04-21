---
title: makemigrations错误
tags: []
id: '438'
categories:
  - - Python
  - - 技术分享
date: 2019-01-04 11:18:56
---

    出错原因：没有再setting.py只指定更改后的USER路径，AUTH\_USER\_MODEL = 'front.User'   manage.py@untitled3 > makemigrations "C:\\Program Files\\JetBrains\\PyCharm 2018.1.4\\bin\\runnerw.exe" C:\\Users\\Administrator\\PycharmProjects\\untitled\\venv\\Scripts\\python.exe "C:\\Program Files\\JetBrains\\PyCharm 2018.1.4\\helpers\\pycharm\\django\_manage.py" makemigrations C:/Users/Administrator/PycharmProjects/untitled3 Tracking file by folder pattern: migrations SystemCheckError: System check identified some issues: ERRORS: auth.User.groups: (fields.E304) Reverse accessor for 'User.groups' clashes with reverse accessor for 'User.groups'. HINT: Add or change a related\_name argument to the definition for 'User.groups' or 'User.groups'. auth.User.user\_permissions: (fields.E304) Reverse accessor for 'User.user\_permissions' clashes with reverse accessor for 'User.user\_permissions'. HINT: Add or change a related\_name argument to the definition for 'User.user\_permissions' or 'User.user\_permissions'. front.User.groups: (fields.E304) Reverse accessor for 'User.groups' clashes with reverse accessor for 'User.groups'. HINT: Add or change a related\_name argument to the definition for 'User.groups' or 'User.groups'. front.User.user\_permissions: (fields.E304) Reverse accessor for 'User.user\_permissions' clashes with reverse accessor for 'User.user\_permissions'. HINT: Add or change a related\_name argument to the definition for 'User.user\_permissions' or 'User.user\_permissions'.