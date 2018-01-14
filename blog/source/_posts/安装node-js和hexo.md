---
title: 安装node.js和hexo
date: 2015-07-15 01:28:42
categories: hexo
tags: [node.js,hexo]
---

### 安装nodeJS之前，如果没有安装g++及 libssl-dev，则先要安装好，安装方法如下：
``` shell
sudo apt-get install g++
sudo apt-get install libssl-dev
```

### 接下来，就可以下载安装nodeJS了，目前稳定版本为 Node.js 0.6.18，下面是安装步骤：
``` shell
wget http://nodejs.org/dist/v0.8.16/node-v0.8.16.tar.gz
tar zxvf node-v0.8.16.tar.gz
./configure
make && make install
```

### 安装好后，在 控制台下输入：
``` shell
node -v
v0.8.16
即可看到安装好的nodeJS版本号
```

-------------------
<!-- more -->

### 更新版本
 node有一个模块叫n，是专门用来管理node.js的版本的。
- 首先安装n模块：
``` shell
npm install -g n
```
- 第二步：
  升级node.js到最新稳定版
``` shell
sudo n stable
```

1. 安装Hexo

Hexo是基于 NodeJS ，所以需要先安装NodeJS。
``` shell
npm install -g hexo-cli

```

2. 初始化框架
``` shell
hexo init <yourFolder>
cd <yourFolder>
```
3. 安装依赖
``` shell
npm install
```
4. 初始化完成大概的目录：
```
.
├── _config.yml //网站的`配置`信息，您可以在此配置大部分的参数。
├── package.json
├── db.json // json格式的静态常量数据库
├── node_modules // Hexo的功能JavaScript文件
├── public // 生成静态网页文件
├── scaffolds //模版文件夹。当您新建文章时，Hexo会根据scaffold来建立文件。
├── source //资源文件夹是存放用户资源的地方。
| ├── _drafts // 草稿文件夹
| └── _posts // 文章文件夹
└── themes //主题文件夹。Hexo会根据主题来生成静态页面。
```
5. 新建文章（创建一个Hello World）
``` shell
hexo new <title> for example: "Hello World"
```
- 在/source/_post里添加hello-world.md文件，之后新建的文章都将存放在此目录下。

- 如果要删除，直接在此文件夹下删除对应的文件即可。

6. 生成网站
``` shell
hexo generate
```
此时会将/source的.md文件生成到/public中，形成网站的静态文件。

7. 服务器
``` shell
hexo server -p 3000
```
输入 http://localhost:3000即可查看网站。

8. 部署网站
``` shell
hexo deploy
```
该操作会将hexo生成的静态内容部署到配置的仓库中，请看下面介绍。

部署网站之前需要生成静态文件，即可以用 $ hexo generate -d 直接生成并部署。

此时需要在 _config.yml 中配置你所要部署的站点：

## Docs: http://hexo.io/docs/deployment.html
deploy:
type: git
repo: git@github.com:YourRepository.git
branch: master
如果没有意外，部署就成功了，可以打开 http://<用户名>.github.io 查看。

### 常用Hexo命令

清除生成内容

> hexo c == hexo clean
执行此操作会删除 public 文件夹中的内容。

> hexo g == hexo generate
> hexo s == hexo server


### 五、使用Next主题让站点更酷炫

1. 使用NexT Theme
``` shell
cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
从Next的Gihub仓库中获取最新版本。

2. Hexo NexT主题的文档结构

```
/languages #用来配置国际化语言版本，里边包含各种个配置像的文本翻译。
/layout #以swig文件来定义各种含有配置信息调用的布局
/scripts #一些JS脚本
/source
/css #用来修改自定义样式，需要掌握一定的css语法。
/fonts #定义字体文件，可以修改博客字体
/images #一些svg图片
/js #一些js脚本
/vendors
/404.html #自定义的公益404页面
/test #用于测试

```

3. 启用NexT主题

需要修改/root/_config.yml配置项theme：

# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: next

4. 验证是否启用

> hexo s --debug
