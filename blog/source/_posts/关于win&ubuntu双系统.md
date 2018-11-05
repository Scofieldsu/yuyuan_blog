title: 关于win7和ubuntu双系统
date: 2015-07-15 01:21:09
categories: 关于一些事儿
tags: 双系统启动

---
###  修改默认启动的系统

ubuntu引导开机，则

sudo gedit /etc/default/grub

GRUB_DEFAULT=0改为开机时显示的win7的排列数字，例如4

sudo update-grub

----
### ubuntu创建快捷方式desktop

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

---

### ubuntu安装deb包
**安装:**  sudo dpkg -i   ****.deb

**解决依赖关系：** sudo  apt-get -f install

**浏览已安装的程序**  dpkg --list

**卸载程序和所有配置文件** sudo apt-get --pure remove <programname>

**只卸载程序，保留配置文** sudo apt-get  remove <programname>
