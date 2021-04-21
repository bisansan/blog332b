---
title: zxinc ipv6数据库python3 解析脚本
tags: []
id: '846'
categories:
  - - Python
abbrlink: f681aab2
date: 2019-09-24 09:12:21
---

修改了官方的python2解析脚本，让它支持python3，目前没有发生什么问题，可以正常使用

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
# @Time    : 2019/9/23 下午3:47
# @Author  : Ryu
# @Site    : 
# @File    : aaa.py
# @Software: PyCharm
import ipaddress
from struct import unpack, unpack_from

NO_IPV4_DB = u"缺少IPv4数据库"

def inet_ntoa(number):
    addresslist=[]
    addresslist.append((number>>24)&0xff)
    addresslist.append((number>>16)&0xff)
    addresslist.append((number>>8)&0xff)
    addresslist.append(number&0xff)
    return ".".join("%d" % i for i in addresslist)


def inet_ntoa6(number):
    addresslist = []
    addresslist.append((number >> 48) & 0xffff)
    addresslist.append((number >> 32) & 0xffff)
    addresslist.append((number >> 16) & 0xffff)
    addresslist.append(number & 0xffff)
    return ":".join("%04X" % i for i in addresslist) + "::"

class find_ip_db():
    def __init__(self):
       # 这里是数据库文件路径
        with open('ipv6wry.db', 'rb') as f:
            self.ip_db = f
            self.ip_db_read = f.read()
        self.indexCount = self.getLong8(8)
        self.firstIndex = self.getLong8(16)
        self.offlen = self.getLong8(6, 1)

    def getLong8(self, offset=0, size=8):
        s = self.ip_db_read[offset: offset + size]
        s += b"\0\0\0\0\0\0\0\0"
        return unpack_from("Q", s)[0]

    def getString(self, offset=0):
        """ 读取字符串信息，包括"国家"信息和"地区"信息

        QQWry.Dat的记录区每条信息都是一个以"\0"结尾的字符串"""

        o2 = self.ip_db_read.find(b"\0", offset)
        # 有可能只有国家信息没有地区信息，
        gb_str = self.ip_db_read[offset:o2]
        try:
            utf8_str = gb_str.decode()
        except:
            return u"未知数据"
        return utf8_str

    def getAreaAddr(self, offset=0):
        """ 通过给出偏移值，取得区域信息字符串，"""
        self_img = self.ip_db_read[offset]
        # self.img[1]

        byte = self_img
        if byte == 1 or byte == 2:
            # 第一个字节为1或者2时，取得2-4字节作为一个偏移量调用自己
            p = self.getLong8(offset + 1, self.offlen)
            return self.getAreaAddr(p)
        else:
            return self.getString(offset)

    def getAddr(self, offset, ip=0):
        img = self.ip_db_read
        o = offset
        byte = img[o]
        if byte == 1:
            # 重定向模式1
            # [IP][0x01][国家和地区信息的绝对偏移地址]
            # 使用接下来的3字节作为偏移量调用字节取得信息
            return self.getAddr(self.getLong8(o + 1, self.offlen))

        else:
            # 重定向模式2 + 正常模式
            # [IP][0x02][信息的绝对偏移][...]
            cArea = self.getAreaAddr(o)
            if byte == 2:
                o += 1 + self.offlen
            else:
                o = self.ip_db_read.find(b"\0", o) + 1
            aArea = self.getAreaAddr(o)
            return (cArea, aArea)

    def find(self, ip, fisrt, end):
        if end - fisrt <= 1:
            return fisrt
        m = int((fisrt + end) / 2)
        o = self.firstIndex + m * (8 + self.offlen)
        new_ip = self.getLong8(o)
        if ip < new_ip:
            return self.find(ip, fisrt, m)
        else:
            return self.find(ip, m, end)

    def find_ip_address(self, ip, i4obj=None):
        ip6 = int(ipaddress.IPv6Address(ip))
        ip = (ip6 >> 64) & 0xFFFFFFFFFFFFFFFF
        i = self.find(ip, 0, self.indexCount)
        o = self.firstIndex + i * (8 + self.offlen)
        o2 = self.getLong8(o + 8, self.offlen)
        (c, a) = self.getAddr(o2)
        (cc, aa) = (c, a)
        i1 = inet_ntoa6(self.getLong8(o))
        try:
            i2 = inet_ntoa6(self.getLong8(o + 8 + self.offlen) - 1)
        except:
            i2 = "FFFF:FFFF:FFFF:FFFF::"
        if ip6 == 0x1:  # 本机地址
            i1 = "0:0:0:0:0:0:0:1"
            i2 = "0:0:0:0:0:0:0:1"
            c = cc = u"本机地址"
        elif ip == 0 and ip6 >> 32 & 0xFFFFFFFF == 0xFFFF:  # IPv4映射地址
            realip = (ip6 & 0xFFFFFFFF)
            realipstr = inet_ntoa(realip)
            try:
                (_, _, realiploc, cc, aa) = i4obj.getIPAddr(realip)
            except:
                realiploc = NO_IPV4_DB
            i1 = "0:0:0:0:0:FFFF:0:0"
            i2 = "0:0:0:0:0:FFFF:FFFF:FFFF"
            c = u"IPv4映射地址"
            a = a + u"<br/>对应的IPv4地址为" + realipstr + u"，位置为" + realiploc
        elif ip >> 48 & 0xFFFF == 0x2002:  # 6to4
            realip = (ip & 0x0000FFFFFFFF0000) >> 16
            realipstr = inet_ntoa(realip)
            try:
                (_, _, realiploc, cc, aa) = i4obj.getIPAddr(realip)
            except:
                realiploc = NO_IPV4_DB
            a = a + u"<br/>对应的IPv4地址为" + realipstr + u"，位置为" + realiploc
        elif ip >> 32 & 0xFFFFFFFF == 0x20010000:  # teredo
            serverip = (ip & 0xFFFFFFFF)
            serveripstr = inet_ntoa(serverip)
            realip = (~ip6 & 0xFFFFFFFF)
            realipstr = inet_ntoa(realip)
            try:
                (_, _, serveriploc, cc, aa) = i4obj.getIPAddr(serverip)
                (_, _, realiploc, _, _) = i4obj.getIPAddr(realip)
            except:
                serveriploc = NO_IPV4_DB
                realiploc = NO_IPV4_DB
            a = a + u"<br/>Teredo服务器的IPv4地址为" + serveripstr + u"，位置为" + serveriploc
            a = a + u"<br/>客户端真实的IPv4地址为" + realipstr + u"，位置为" + realiploc
        elif ip6 >> 32 & 0xFFFFFFFF == 0x5EFE:  # isatap
            realip = (ip6 & 0xFFFFFFFF)
            realipstr = inet_ntoa(realip)
            try:
                (_, _, realiploc, _, _) = i4obj.getIPAddr(realip)
            except:
                realiploc = NO_IPV4_DB
            a = a + u"<br/>ISATAP地址，对应的IPv4地址为" + realipstr + u"，位置为" + realiploc
        return i1, i2, c + u" " + a, cc, aa

print(find_ip_db().find_ip_address('2409:894c:c38:7f65:a413:9f69:2810:9d6a'))
```