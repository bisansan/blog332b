---
title: Ubuntu 添加∬上网方法
tags: []
id: '819'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
date: 2019-08-21 11:53:45
---

ubuntu直接添加下列PPA源

```
sudo add-apt-repository ppa:hzwhuang/∬-qt5      #请将∬替换成ss
sudo apt-get update
sudo apt-get install ∬ocks-qt5        # 请将∬ 替换成$hadow$，再将美元符号换成s
```

更改源文件，然后再安装，如果是Ubuntu 18 代号Bionic，会报错因为目前只有到16 （代号xenial）

```
cd /etc/apt/sources.list.d/
sudo apt install gedit
sudo geditl hzwhuang-ubuntu-∬-qt5-bionic.list       # 请将∬替换成两个s隔开s

# 打开该文件后，将原有的bionic改成xenial。
```

设置PAC上网模式

你的电脑得具有python环境，并且已经安装了pip并升级最新版本

```
# 安装genpac
pip install genpac
```

2.生成auto.pac文件  
随便放那个路径自己决定了，比如~/PAC/

```
mkdir ~/PAC/

cd ~/PAC/

touch user-rules.txt

genpac -p "SOCK(?) 127.0.0.1:1090" --gf(@)ist-(!)xy="SOCK(?) 127.0.0.1:1090" --output="auto(!).pac" --gf(@)ist-url="https://raw.githubusercontent.com/gf(@)ist/gf(@)ist/master/gf(@)ist.txt"

# GenPACDeprecationWarning: 在2.0中参数-p已被--pac-(!)xy取代, 后续版本将删除, 避免使用.

#  将(!)替换成pro, 将(?)替换成S5，将(@)替换成wl
# 对应的端口可以自己设置，比如我的是1090
```

点进网络设置，设置如下：  
`file:///~/PAC/auto.pac`

chrome 上网启动方法

```
#  直接用root权限启动
sudo google-chrome --(!)xy-server=“socks://127.0.0.1:1090” --no-sandbox --user-data-dir

# 用户权限启动

google-chrome --(!)xy-server="socks://127.0.0.1:1090"

#  将(!)替换成pro, 将(?)替换成S5，将(@)替换成wl
```

更详细的参考下面

[https://www.linuxdashen.com/%e5%9c%a8%e5%91%bd%e4%bb%a4%e8%a1%8c%e4%b8%8b%e4%b8%bachromium%e5%92%8cgoogle-chrome%e6%b5%8f%e8%a7%88%e5%99%a8%e8%ae%be%e7%bd%ae%e4%bb%a3%e7%90%86](https://www.linuxdashen.com/%e5%9c%a8%e5%91%bd%e4%bb%a4%e8%a1%8c%e4%b8%8b%e4%b8%bachromium%e5%92%8cgoogle-chrome%e6%b5%8f%e8%a7%88%e5%99%a8%e8%ae%be%e7%bd%ae%e4%bb%a3%e7%90%86)