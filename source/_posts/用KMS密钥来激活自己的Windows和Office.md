---
title: 用KMS密钥来激活自己的Windows和Office
tags: [kms激活,windows]
id: '668'
categories:
  - - 技术教程
abbrlink: cdddeb77
date: 2018-03-24 03:37:00
---

先要找到对面的KEY：[https://technet.microsoft.com/en-us/library/jj612867.aspx](https://technet.microsoft.com/en-us/library/jj612867.aspx)

然后用管理员权限运行CMD，依次输入命令

Windows系统激活命令  
slmgr.vbs -upk

slmgr.vbs -ipk W269N-WFGWX-YVC9B-4J6C9-T83GX

这里填入你对应的key

slmgr.vbs -skms kms.dwhd.org

这里填入对应的KMS服务器地址，没有请自己百度找

slmgr.vbs -ato

slmgr.vbs -dlv

Office激活命令  
1.使用 命令提示符（CMD）管理员模式 执行命令(若Office安装在其他盘符，请自行将C改为对应盘符)  
cd "C:Program FilesMicrosoft OfficeOffice14" 【Office2010】  
cd "C:Program FilesMicrosoft OfficeOffice15" 【Office2013】  
cd "C:Program FilesMicrosoft OfficeOffice16" 【Office2016】

2.执行命令设置Office的KMS服务器地址

cscript ospp.vbs /sethst:kms.chinancce.com

3.执行命令激活Office

cscript ospp.vbs /act

4.(可选)执行命令查询Office激活时间

cscript ospp.vbs /dstatus

Windows 10系统自动激活程序下载，3KB大小2017年9月份亲测可用    

下载地址：Win10\_KMS\_Activation[Win10\_KMS\_Activation.zip](http://post.332b.com/usr/uploads/2018/03/3058077553.zip)