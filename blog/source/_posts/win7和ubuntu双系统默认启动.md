---
title: win7和ubuntu双系统默认启动
date: 2015-07-15 01:21:09
categories: ubuntu
tags: 双系统启动
---

ubuntu引导开机，则

sudo gedit /etc/default/grub

GRUB_DEFAULT=0改为开机时显示的win7的排列数字，例如4

sudo update-grub

