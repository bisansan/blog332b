---
title: ubuntu将台式机和手机结合，变成无线耳机
tags: []
id: '626'
categories:
  - - '%e7%94%b5%e8%84%91%e7%b3%bb%e7%bb%9f'
    - ubuntu
  - - 技术分享
abbrlink: 2dd0534
date: 2019-04-09 10:56:55
---

安装PortAudio是一款专为跨平台设计的便携式音频I / O库

```
sudo apt-get install portaudio19-dev
```

安装libcurl

sudo apt-get install libcurl4

安装pavucontrol

sudo apt-get install pavucontrol

安装libcurl `sudo apt-get install libcurl4 curl` 为了能在命令行使用Soundwire，将Soundwire文件夹添加到环境变量 `sudo vim /etc/profile` 在末尾添加,下面替换成你自己的路径： `export PATH=$PATH:/home/sky/software/SoundWireServer` 使配置生效： `source /etc/profile` 这样以来，就可以在命令行输入: `SoundWireServer` 打开Soundwire了，如果不想使用图形界面，可以加上-nogui参数： `SoundWireServer -nogui`

  创建图标

sudo gedit /usr/share/applications/SoundWire-Server.desktop

#配置文件如下
#!/usr/bin/env xdg-open

\[Desktop Entry\]
Name=SoundWire Server
Comment=Server program for SoundWire Android app
Exec=/home/witt/soft/SoundWireServer/SoundWireServer
Icon=/home/witt/soft/SoundWireServer/sw-icon.xpm
Terminal=false
Type=Application
Categories=AudioVideo;Audio