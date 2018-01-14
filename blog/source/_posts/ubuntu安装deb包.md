---
title: ubuntu安装deb包
date: 2015-07-15 01:23:13
categories: ubuntu
---
**安装:**  sudo dpkg -i   ****.deb

**解决依赖关系：** sudo  apt-get -f install

**浏览已安装的程序**  dpkg --list

**卸载程序和所有配置文件** sudo apt-get --pure remove <programname>

**只卸载程序，保留配置文** sudo apt-get  remove <programname>


