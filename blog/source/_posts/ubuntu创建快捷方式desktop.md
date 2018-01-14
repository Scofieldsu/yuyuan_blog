---
title: ubuntu创建快捷方式desktop
date: 2015-07-15 01:13:57
categories: ubuntu
tags: ubuntu 
---
#ubuntu创建快捷方式desktop
**例如**
把Ulipad添加到系统的“应用程序”菜单里，方法如下：
'sudo gedit /usr/share/applications/Ulipad.desktop'
然后在里面添加如下内容：

[Desktop Entry]
Name=Ulipad
Comment=a Python IDE
Exec=python /home/scofireldyu/下载/ulipad/UliPad.py
Icon=/home/scofireldyu/下载/ulipad/ulipad.ico
Teminal=false
Type=Application
Categories=Application;Development;
