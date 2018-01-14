---
title: vue.js入门
date: 2017-06-01 22:39:08
categories: frontend
tags: [vue.js,npm,elementUI,axios,vuex]
---

###  安装

1.下载node.js安装

2.打开命令行 npm init ，输入相应信息，系统用户路径生成npm.json文件作为默认配置

3.配置npm的taobao源，加快安装速度：  npm config set registry http://registry.npm.taobao.org/

4.安装vue： npm install vue

5.安装vue脚手架，快速搭建项目结构： npm install --global vue-cli

6.开始你的项目：vue init webpack your-project-name

7.安装依赖：

cd  your-project-name

npm install

- 运行
npm run dev

- 构建
npm build
<!-- more -->

### 项目代码结构

- build
- config
- dist
- inspectionProfiles
- noode_modules
- src
  - assets
  - components
  - App.vue
  - main.js
- static 
- test
- theme
- ...
- index.html
- package.json

>- 其中npm install 是根据package.json中依赖安装模块到node_modules路径下。
>- npm run dev 会自动打开浏览器显示你的页面。
>- npm run build 会在dist路径下生成index.html和static文件夹，static里包括css，js，font。一般把dist中内容结合服务端显示。

### 学习vue的常用插件

- vue官网:http://cn.vuejs.org/v2/guide/

- vue-router(官方路由插件): https://router.vuejs.org/zh-cn/

- axios(ajax插件): http://www.kancloud.cn/yunye/axios/234845

- 界面UI: http://element.eleme.io/#/zh-CN/component/installation

- 树形控件ztree:  http://www.treejs.cn/v3/main.php#_zTreeInfo

- vuex(全局状态管理): https://vuex.vuejs.org/zh-cn/

### 推荐学习路线
1. 安装完成后，可以根据网上视频学习做出简单的todolist，用来熟悉开发过程。
2. 从github学习vue-admin项目，了解多页面系统怎么使用插件。
3. 可以自由使用插件搭建你想做的应用。
4. 学习插件的使用可以帮你更好的完成目标，学习github上项目的代码结构，帮助你在开发复杂项目时有条不紊。

