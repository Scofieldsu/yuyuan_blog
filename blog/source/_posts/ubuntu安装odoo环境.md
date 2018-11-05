---
title: 关于ubuntu安装odoo环境
date: 2016-12-08 21:13:45
categories: 关于一些事儿
tags: [odoo,ubuntu,postgresql,python]
---
# ubuntu安装odoo环境
  接触odoo几个月的期间，刚开始装环境也是缺东少西，按照文档一步一步来，后来慢慢理解了需要装什么，哪些是必要的。自己工作中使用了ubuntu系统，后来换成mac也在mac上装了环境，不同人安装可能遇到的问题也不一样，但只要知道我们需要什么，就万变不离其宗，我认为可以分为这几块：odoo源码；postgresql数据库；nodejs和less；运行odoo环境的python依赖包。
   于是可以围绕这几点开始安装。第一，odoo源码。建议从github上clone下来 odoo9或odoo10源码。两者的目录结构有细微变动，而且在启动服务时运行的文件不一样。odoo9运行的是odoo.py，其配置文件是odoo-9.0/debian/openerp-server.conf，odoo10运行的是odoo.bin,其配置文件是odoo10/debian/odoo.conf。第二安装postgresql数据库。ubuntu可以命令行安装，mac上可以下载postgresql.app比较方便。第三nodejs和lessc参照其他网上教程。第四安装运行需要的python依赖包，网上有个requirement.txt一次运行安装所有依赖包，对于没有安装成功的包，具体问题具体分析对待。

-  安装postgresql：sudo  apt-get install postgresql  ;

- 检查安装：psql --version

-  安装pip: sudo apt-get install python-pip

- 切换postgres用户：sudo  su - postgres

- 创建新的数据库用户yuyuan：createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt yuyuan

- 退出用户：exit

- 安装各个依赖包：sudo apt-get install python-dateutil python-docutils python-feedparser python-gdata
- python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid
- python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing
- python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject
- python-webdav python-werkzeug python-xlwt python-yaml python-zsi python-pyPdf
- python-decorator python-passlib python-requests

- 其中pypdf如不能安装，www.python.org下载pyPdf.tar.gz  解压  tar zxvf  pyPdf.tar.gz,进入文件夹，sudo python setup.py install

- 安装nodes：sudo apt -get install nodes-legacy;sudo apt install -y npm;sudo npm install -g less less-plugin-clean-css;sudo ln -s /usr/bin/nodejs  /usr/bin/node

- 安装git ：sudo apt-get install git

- 进入某个目录：git clone -b 9.0 https://github.com/odoo/odoo.git  .

- 安装pgadmin3: sudo apt-get  install pgadmin3

- 安装sublime text3：sudo add-apt-repository ppa:webupd8team/sublime-text-3；sudo apt-get update ；sudo apt-get install sublime-text-installer
